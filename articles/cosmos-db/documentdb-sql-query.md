---
title: query aaaSQL per l'API DocumentDB DB Cosmos Azure | Documenti Microsoft
description: "Informazioni sulla sintassi SQL, sui concetti relativi ai database e sulle query SQL per Cosmos DB. SQL può essere usato come linguaggio di query JSON in Cosmos DB."
keywords: sintassi sql, query sql, linguaggio di query json, concetti relativi ai database e query sql, funzioni di aggregazione
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="eeadf-105">Query SQL per l'API di DocumentDB di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eeadf-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="eeadf-106">Microsoft Azure Cosmos DB supporta l'esecuzione di query di documenti mediante SQL (Structured Query Language) come linguaggio di query JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="eeadf-107">Cosmos DB è effettivamente privo di schema.</span><span class="sxs-lookup"><span data-stu-id="eeadf-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="eeadf-108">In virtù del relativo commit toohello JSON modello di dati direttamente nel motore di database hello, fornisce l'indicizzazione automatica di documenti JSON senza richiedere uno schema esplicito o la creazione di indici secondari.</span><span class="sxs-lookup"><span data-stu-id="eeadf-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="eeadf-109">Durante la progettazione di linguaggio di query hello per Cosmos DB, abbiamo due obiettivi:</span><span class="sxs-lookup"><span data-stu-id="eeadf-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="eeadf-110">Invece di realizzazione di un nuovo linguaggio di query JSON, Desideravamo toosupport SQL.</span><span class="sxs-lookup"><span data-stu-id="eeadf-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="eeadf-111">SQL è uno dei linguaggi di query più più comuni di hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="eeadf-112">Il linguaggio di query SQL di Cosmos DB fornisce un modello di programmazione formale per le query complesse sui documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="eeadf-113">Come un database di documenti JSON in grado di eseguire JavaScript direttamente nel motore di database hello, Desideravamo modello di programmazione toouse JavaScript di base hello per il linguaggio di query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="eeadf-114">Hello DocumentDB API SQL è una radice nel sistema di tipi di JavaScript, la valutazione dell'espressione e chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="eeadf-115">Questo rappresenta a sua volta un modello di programmazione naturale per le proiezioni relazionali, la navigazione gerarchica attraverso i documenti JSON, i self join, query spaziali e la chiamata di funzioni definite dall'utente (UDF) scritte interamente in JavaScript, tra le altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eeadf-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="eeadf-116">Riteniamo che queste funzionalità sono tooreducing chiave le forze di attrito hello tra un'applicazione hello e database hello e sono fondamentali per la produttività degli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="eeadf-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="eeadf-117">Si consiglia di introduzione osservando i seguenti video, in cui Aravind Ramachandran illustra le funzionalità di query del DB Cosmos, hello e visitare il nostro [Query Playground](http://www.documentdb.com/sql/demo), in cui è possibile provare Cosmos DB ed eseguire query SQL il set di dati.</span><span class="sxs-lookup"><span data-stu-id="eeadf-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="eeadf-118">Tornare quindi toothis articolo, in cui si inizia con un'esercitazione di query SQL che illustra alcune semplici documenti JSON e i comandi SQL.</span><span class="sxs-lookup"><span data-stu-id="eeadf-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="eeadf-119"><a id="GettingStarted"></a>Guida introduttiva ai comandi SQL in Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eeadf-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="eeadf-120">toosee Cosmos DB SQL a livello di lavoro, si inizia con alcuni documenti JSON semplici e seguire i passaggi alcune semplici query su di esso.</span><span class="sxs-lookup"><span data-stu-id="eeadf-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="eeadf-121">Considerare questi due documenti JSON come se riguardassero due famiglie.</span><span class="sxs-lookup"><span data-stu-id="eeadf-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="eeadf-122">Con Cosmos DB, non è necessario toocreate eventuali schemi o gli indici secondari in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="eeadf-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="eeadf-123">È sufficiente tooinsert hello JSON documenti tooa DB Cosmos raccolta e quindi eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="eeadf-124">Qui abbiamo un JSON semplice documento per hello famiglia Andersen, hello padri, figli (e gli animali domestici), l'indirizzo e informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="eeadf-125">documento di Hello contiene stringhe, numeri, valori booleani, matrici e proprietà annidate.</span><span class="sxs-lookup"><span data-stu-id="eeadf-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="eeadf-126">**Documento**</span><span class="sxs-lookup"><span data-stu-id="eeadf-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="eeadf-127">Ecco un secondo documento con una sottile differenza: vengono usati `givenName` e `familyName` invece di `firstName` e `lastName`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="eeadf-128">**Documento**</span><span class="sxs-lookup"><span data-stu-id="eeadf-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="eeadf-129">Ora provare alcune query su questa toounderstand dati alcune hello agli aspetti principali di SQL API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="eeadf-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="eeadf-130">Ad esempio, eseguire una query restituisce i documenti hello in campo id hello corrisponde seguente hello `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="eeadf-131">Poiché si tratta di un `SELECT *`, output di hello di query hello è documento JSON completo hello:</span><span class="sxs-lookup"><span data-stu-id="eeadf-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="eeadf-132">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-133">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="eeadf-134">Ora si consideri il caso di hello in cui è necessario tooreformat hello output JSON in una forma diversa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="eeadf-135">Questa query progetti JSON un nuovo oggetto con due campi selezionati, nome e la città, quando hello degli città ha hello stesso nome come stato hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="eeadf-136">In questo caso, "NY, NY" corrispondono.</span><span class="sxs-lookup"><span data-stu-id="eeadf-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="eeadf-137">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="eeadf-138">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="eeadf-139">la query successiva Hello restituisce tutti i nomi di hello specificato di elementi figlio nella famiglia di hello il cui id corrisponde `WakefieldFamily` ordinati in base alla città hello di residenza.</span><span class="sxs-lookup"><span data-stu-id="eeadf-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="eeadf-140">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="eeadf-141">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="eeadf-142">Desideriamo toodraw attenzione tooa alcuni aspetti importanti di hello Cosmos DB linguaggio esempi hello che abbiamo visto finora di query:</span><span class="sxs-lookup"><span data-stu-id="eeadf-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="eeadf-143">Poiché l'API SQL di DocumentDB elabora i valori JSON, deve gestire entità con struttura ad albero invece di righe e colonne.</span><span class="sxs-lookup"><span data-stu-id="eeadf-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="eeadf-144">Di conseguenza, il linguaggio di hello consente di fare riferimento toonodes della struttura ad albero hello a qualsiasi profondità arbitraria, ad esempio `Node1.Node2.Node3…..Nodem`, simile toorelational SQL che fa riferimento toohello due riferimento alla parte di `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="eeadf-145">Hello structured query language funziona con i dati senza schema.</span><span class="sxs-lookup"><span data-stu-id="eeadf-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="eeadf-146">Pertanto, hello toobe associazione di tipo sistema esigenze in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="eeadf-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="eeadf-147">Hello stessa espressione potrebbe restituire tipi diversi in diversi documenti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="eeadf-148">risultato Hello di una query è un valore JSON valido, ma non è garantito toobe di uno schema fisso.</span><span class="sxs-lookup"><span data-stu-id="eeadf-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="eeadf-149">Cosmos DB supporta solo i documenti JSON completi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="eeadf-150">Ciò significa espressioni e il sistema di tipi di hello toodeal limitate solo con tipi JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="eeadf-151">Fare riferimento toohello [specifica JSON](http://www.json.org/) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="eeadf-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="eeadf-152">Una raccolta di Cosmos DB è un contenitore senza schema dei documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="eeadf-153">le relazioni di Hello in entità di dati all'interno di documenti in una raccolta in modo implicito vengono acquisite dal contenuto e non da chiave primaria e relazioni di chiave esterne.</span><span class="sxs-lookup"><span data-stu-id="eeadf-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="eeadf-154">Questo è un aspetto importante importante precisare alla luce di join tra più documenti hello descritto più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="eeadf-155"><a id="Indexing"></a> Indicizzatore di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eeadf-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="eeadf-156">Prima di passare a hello sintassi SQL API DocumentDB, vale la pena esplorazione hello l'indicizzazione di progettazione in DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eeadf-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="eeadf-157">scopo di Hello degli indici dei database è tooserve query nei vari moduli e forme con un consumo di risorse minime (ad esempio CPU e di input/output) fornendo una velocità effettiva ottimale e a bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="eeadf-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="eeadf-158">Spesso, scelta hello dell'indice di destra hello per le query di un database richiede una quantità pianificazione e sperimentazione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="eeadf-159">Questo approccio pone un problema per i database senza schema in cui i dati hello tooa strict schema non è conforme e si evolve rapidamente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="eeadf-160">Pertanto, quando è stato progettato sottosistema di indicizzazione Cosmos DB hello, impostiamo hello seguenti obiettivi:</span><span class="sxs-lookup"><span data-stu-id="eeadf-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="eeadf-161">Indicizzare i documenti senza schema: hello indicizzazione sottosistema non richiede alcuna informazione sullo schema o supposizioni sullo schema di documenti hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="eeadf-162">Supporto per le query relazionale e gerarchiche efficiente e complesse: indice hello supporta il linguaggio di query Cosmos DB hello in modo efficiente, incluso il supporto per le proiezioni relazionale e gerarchiche.</span><span class="sxs-lookup"><span data-stu-id="eeadf-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="eeadf-163">Supporto per le query coerente riscontri un volume velocità delle operazioni di scrittura: per la scrittura ad alta velocità effettiva dei carichi di lavoro con query coerente, hello indice viene aggiornato in modo incrementale, in modo efficiente e online in faccia hello di un volume velocità delle operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="eeadf-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="eeadf-164">aggiornamento di un indice coerente Hello è query hello tooserve fondamentale a livello di coerenza hello in quale servizio di documenti hello hello configurato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="eeadf-165">Supporto per multi-tenancy: dato modello basato su prenotazione hello di governance delle risorse tra i tenant, gli aggiornamenti dell'indice vengono eseguiti all'interno del budget hello delle risorse di sistema (CPU, memoria e operazioni di input/output al secondo) allocata per ogni replica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="eeadf-166">L'efficienza di archiviazione: per convenienza economica rispetto a, hello archiviazione su disco overhead dell'indice hello è limitata e prevedibile.</span><span class="sxs-lookup"><span data-stu-id="eeadf-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="eeadf-167">Ciò è fondamentale poiché DB Cosmos consente hello developer toomake basato sui costi dei compromessi tra overhead delle prestazioni delle query di relazione toohello dell'indice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="eeadf-168">Fare riferimento toohello [esempi Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) in MSDN per gli esempi che mostra come tooconfigure hello criteri di indicizzazione per una raccolta.</span><span class="sxs-lookup"><span data-stu-id="eeadf-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="eeadf-169">Consente ora ottenere i dettagli di hello di hello sintassi SQL di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eeadf-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="eeadf-170"><a id="Basics"></a>Elementi di base di una query SQL di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eeadf-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="eeadf-171">Ogni query consiste in una clausola SELECT e clausole FROM e WHERE facoltative in base agli standard ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="eeadf-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="eeadf-172">In genere, per ogni query, hello source nella clausola FROM hello enumerato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="eeadf-173">Quindi hello applicare un filtro nella clausola WHERE viene applicata in hello origine tooretrieve hello un sottoinsieme di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="eeadf-174">Infine, in cui viene utilizzata la clausola SELECT hello hello tooproject richiesti i valori JSON nel hello selezionare nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="eeadf-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="eeadf-175"><a id="FromClause"></a>Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="eeadf-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="eeadf-176">Hello `FROM <from_specification>` clausola è facoltativa a meno che l'origine hello è filtrato o previsto in un secondo momento nella query di hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="eeadf-177">scopo di Hello di questa clausola è origine di dati di hello toospecify al quale hello deve utilizzare query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="eeadf-178">In genere insieme hello è origine hello, ma uno può specificare un subset della raccolta hello invece.</span><span class="sxs-lookup"><span data-stu-id="eeadf-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="eeadf-179">Ad esempio una query `SELECT * FROM Families` indica che l'intera raccolta di gruppi hello è origine hello su quali tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="eeadf-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="eeadf-180">Un identificatore speciale radice può essere utilizzato toorepresent hello insieme anziché il nome di raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="eeadf-181">Hello elenco seguente contiene le regole di hello che vengono applicate per ogni query:</span><span class="sxs-lookup"><span data-stu-id="eeadf-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="eeadf-182">raccolta di Hello può essere utilizzato un alias, ad esempio `SELECT f.id FROM Families AS f` o semplicemente `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="eeadf-183">Qui `f` equivalente hello `Families`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="eeadf-184">`AS`è un identificatore di hello tooalias la parola chiave facoltativa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="eeadf-185">Una volta associato un alias, non è possibile associare l'origine originale hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="eeadf-186">Ad esempio, `SELECT Families.id FROM Families f` la sintassi è valida perché non è possibile risolvere più identificatore hello "Gruppi".</span><span class="sxs-lookup"><span data-stu-id="eeadf-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="eeadf-187">Tutte le proprietà che devono toobe a cui fa riferimento devono essere completi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="eeadf-188">In assenza di hello di conformità rigorosa dello schema, questo viene imposto tooavoid tutte le associazioni ambigue.</span><span class="sxs-lookup"><span data-stu-id="eeadf-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="eeadf-189">Pertanto, `SELECT id FROM Families f` la sintassi è valida perché la proprietà hello `id` non è associato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="eeadf-190">Documenti secondari</span><span class="sxs-lookup"><span data-stu-id="eeadf-190">Subdocuments</span></span>
<span data-ttu-id="eeadf-191">origine Hello può rivelarsi sottoinsieme più piccolo tooa ridotta.</span><span class="sxs-lookup"><span data-stu-id="eeadf-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="eeadf-192">Ad esempio, solo un sottoalbero in ogni documento tooenumerating, subroot hello quindi causare origine hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="eeadf-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="eeadf-193">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="eeadf-194">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="eeadf-195">Mentre hello sopra riportato di seguito viene utilizzata una matrice come origine di hello, un oggetto potrebbe inoltre essere utilizzato come origine di hello, ovvero quello mostrato nell'esempio seguente hello: qualsiasi valore JSON valido (non definito) che può essere trovati nell'origine hello viene considerato per l'inclusione nel risultato hello query Hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="eeadf-196">Se non dispone di alcune famiglie un `address.state` valore, sono escluse hello risultato della query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="eeadf-197">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="eeadf-198">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="eeadf-199"><a id="WhereClause"></a>Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="eeadf-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="eeadf-200">clausola WHERE Hello (**`WHERE <filter_condition>`**) è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="eeadf-201">Specifica hello verificate che documenti JSON hello forniti dall'origine hello devono soddisfare in ordine toobe incluso come parte del risultato hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="eeadf-202">Deve restituire un documento JSON hello specificato condizioni troppo "true" toobe presi in considerazione per il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="eeadf-203">Hello dove clausola viene utilizzata dal livello di indice hello in ordine toodetermine hello assoluto subset più piccolo di documenti di origine che possono far parte del risultato hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="eeadf-204">la query seguente Hello richiede documenti che contengono una proprietà name il cui valore è `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="eeadf-205">Qualsiasi altro tipo di documento che non dispone di una proprietà name, o in cui non corrisponde al valore di hello `AndersenFamily` è escluso.</span><span class="sxs-lookup"><span data-stu-id="eeadf-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="eeadf-206">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-207">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="eeadf-208">Hello precedente riportato di seguito viene riportata una query semplice uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="eeadf-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="eeadf-209">L'API SQL di DocumentDB supporta anche una varietà di espressioni scalari.</span><span class="sxs-lookup"><span data-stu-id="eeadf-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="eeadf-210">Hello più comunemente usato sono espressioni di binari e unari.</span><span class="sxs-lookup"><span data-stu-id="eeadf-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="eeadf-211">Anche i riferimenti di proprietà da un oggetto JSON di origine hello sono espressioni valide.</span><span class="sxs-lookup"><span data-stu-id="eeadf-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="eeadf-212">Hello dopo gli operatori binari è attualmente supportato e possa essere utilizzata nelle query come illustrato nell'hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="eeadf-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="eeadf-213">Aritmetico</span><span class="sxs-lookup"><span data-stu-id="eeadf-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="eeadf-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="eeadf-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eeadf-215">Bit per bit</span><span class="sxs-lookup"><span data-stu-id="eeadf-215">Bitwise</span></span></td>    
<td><span data-ttu-id="eeadf-216">|, &, ^, <<, >>, >>> (spostamento a destra riempimento zero)</span><span class="sxs-lookup"><span data-stu-id="eeadf-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eeadf-217">Logico</span><span class="sxs-lookup"><span data-stu-id="eeadf-217">Logical</span></span></td>
<td><span data-ttu-id="eeadf-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="eeadf-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eeadf-219">Confronto</span><span class="sxs-lookup"><span data-stu-id="eeadf-219">Comparison</span></span></td>    
<td><span data-ttu-id="eeadf-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="eeadf-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eeadf-221">String</span><span class="sxs-lookup"><span data-stu-id="eeadf-221">String</span></span></td>    
<td><span data-ttu-id="eeadf-222">|| (concatenazione)</span><span class="sxs-lookup"><span data-stu-id="eeadf-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="eeadf-223">Saranno ora prese in esame alcune query che usano gli operatori binari.</span><span class="sxs-lookup"><span data-stu-id="eeadf-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="eeadf-224">Hello operatori unari +,-, ~ non sono supportate anche e può essere utilizzata all'interno di query come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="eeadf-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="eeadf-225">Toobinary e gli operatori unari, sono inoltre consentiti anche i riferimenti di proprietà.</span><span class="sxs-lookup"><span data-stu-id="eeadf-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="eeadf-226">Ad esempio, `SELECT * FROM Families f WHERE f.isRegistered` restituisce hello documento JSON che contiene proprietà hello `isRegistered` in cui il valore della proprietà hello è uguale toohello JSON `true` valore.</span><span class="sxs-lookup"><span data-stu-id="eeadf-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="eeadf-227">Tutti gli altri valori (false, null, non è definito, `<number>`, `<string>`, `<object>`, `<array>`e così via) comporta i documento di origine toohello viene escluso dal risultato hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="eeadf-228">Operatori di confronto e uguaglianza</span><span class="sxs-lookup"><span data-stu-id="eeadf-228">Equality and comparison operators</span></span>
<span data-ttu-id="eeadf-229">Hello nella tabella seguente mostra hello risultato dei confronti di uguaglianza in DocumentDB API SQL tra qualsiasi due tipi JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="eeadf-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="eeadf-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="eeadf-233">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="eeadf-234">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="eeadf-235">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="eeadf-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="eeadf-237">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="eeadf-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-254">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="eeadf-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-262">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="eeadf-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-270">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="eeadf-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="eeadf-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="eeadf-286">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="eeadf-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="eeadf-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="eeadf-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="eeadf-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="eeadf-294">Per altri operatori di confronto, ad esempio >, > =,! =, < e < =, hello si applicano le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="eeadf-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="eeadf-295">Confronto tra risultati dei tipi in Undefined.</span><span class="sxs-lookup"><span data-stu-id="eeadf-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="eeadf-296">Confronto tra i risultati di due oggetti o due matrici in Undefined.</span><span class="sxs-lookup"><span data-stu-id="eeadf-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="eeadf-297">Se il risultato di hello dell'espressione scalare di hello nel filtro hello è definito, documento corrispondente hello non viene incluso nel risultato hello, poiché non definito in modo logico non equivalgono troppo "true".</span><span class="sxs-lookup"><span data-stu-id="eeadf-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="eeadf-298">Parola chiave BETWEEN</span><span class="sxs-lookup"><span data-stu-id="eeadf-298">BETWEEN keyword</span></span>
<span data-ttu-id="eeadf-299">È inoltre possibile utilizzare hello BETWEEN parola chiave tooexpress le query su intervalli di valori come in SQL ANSI.</span><span class="sxs-lookup"><span data-stu-id="eeadf-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="eeadf-300">La parola BETWEEN può essere utilizzata con stringhe o numeri.</span><span class="sxs-lookup"><span data-stu-id="eeadf-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="eeadf-301">Ad esempio, questa query restituisce tutti i documenti della famiglia in cui hello livello prima del bambino è compreso tra 1 e 5 (inclusi).</span><span class="sxs-lookup"><span data-stu-id="eeadf-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="eeadf-302">A differenza di ANSI-SQL, è possibile utilizzare anche clausola BETWEEN hello nella clausola FROM di hello come nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="eeadf-303">Per i tempi di esecuzione query, tenere presente che un criterio di indicizzazione che utilizza un tipo di indice di intervallo su qualsiasi proprietà o i percorsi numerici che vengono filtrati nella clausola BETWEEN hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="eeadf-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="eeadf-304">Hello la differenza principale tra l'utilizzo di BETWEEN API DocumentDB e di SQL ANSI è che è possibile esprimere le query di intervallo rispetto alle proprietà di tipi misti: ad esempio, potrebbe essere "livello" essere un numero (5) alcuni documenti e le stringhe in altri ambienti ("grade4").</span><span class="sxs-lookup"><span data-stu-id="eeadf-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="eeadf-305">In questi casi, ad esempio in JavaScript, un confronto tra due tipi diversi risultati "undefined" e il documento hello verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="eeadf-306">Operatori logici (AND, OR e NOT)</span><span class="sxs-lookup"><span data-stu-id="eeadf-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="eeadf-307">Gli operatori logici funzionano con valori booleani.</span><span class="sxs-lookup"><span data-stu-id="eeadf-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="eeadf-308">tabelle verità logiche Hello per questi operatori vengono visualizzate in hello le tabelle seguenti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="eeadf-309">OPPURE</span><span class="sxs-lookup"><span data-stu-id="eeadf-309">OR</span></span> | <span data-ttu-id="eeadf-310">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-310">True</span></span> | <span data-ttu-id="eeadf-311">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-311">False</span></span> | <span data-ttu-id="eeadf-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eeadf-313">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-313">True</span></span> |<span data-ttu-id="eeadf-314">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-314">True</span></span> |<span data-ttu-id="eeadf-315">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-315">True</span></span> |<span data-ttu-id="eeadf-316">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-316">True</span></span> |
| <span data-ttu-id="eeadf-317">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-317">False</span></span> |<span data-ttu-id="eeadf-318">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-318">True</span></span> |<span data-ttu-id="eeadf-319">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-319">False</span></span> |<span data-ttu-id="eeadf-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-320">Undefined</span></span> |
| <span data-ttu-id="eeadf-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-321">Undefined</span></span> |<span data-ttu-id="eeadf-322">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-322">True</span></span> |<span data-ttu-id="eeadf-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-323">Undefined</span></span> |<span data-ttu-id="eeadf-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-324">Undefined</span></span> |

| <span data-ttu-id="eeadf-325">AND</span><span class="sxs-lookup"><span data-stu-id="eeadf-325">AND</span></span> | <span data-ttu-id="eeadf-326">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-326">True</span></span> | <span data-ttu-id="eeadf-327">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-327">False</span></span> | <span data-ttu-id="eeadf-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eeadf-329">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-329">True</span></span> |<span data-ttu-id="eeadf-330">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-330">True</span></span> |<span data-ttu-id="eeadf-331">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-331">False</span></span> |<span data-ttu-id="eeadf-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-332">Undefined</span></span> |
| <span data-ttu-id="eeadf-333">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-333">False</span></span> |<span data-ttu-id="eeadf-334">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-334">False</span></span> |<span data-ttu-id="eeadf-335">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-335">False</span></span> |<span data-ttu-id="eeadf-336">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-336">False</span></span> |
| <span data-ttu-id="eeadf-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-337">Undefined</span></span> |<span data-ttu-id="eeadf-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-338">Undefined</span></span> |<span data-ttu-id="eeadf-339">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-339">False</span></span> |<span data-ttu-id="eeadf-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-340">Undefined</span></span> |

| <span data-ttu-id="eeadf-341">NOT</span><span class="sxs-lookup"><span data-stu-id="eeadf-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="eeadf-342">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-342">True</span></span> |<span data-ttu-id="eeadf-343">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-343">False</span></span> |
| <span data-ttu-id="eeadf-344">False</span><span class="sxs-lookup"><span data-stu-id="eeadf-344">False</span></span> |<span data-ttu-id="eeadf-345">True</span><span class="sxs-lookup"><span data-stu-id="eeadf-345">True</span></span> |
| <span data-ttu-id="eeadf-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-346">Undefined</span></span> |<span data-ttu-id="eeadf-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="eeadf-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="eeadf-348">Parola chiave IN</span><span class="sxs-lookup"><span data-stu-id="eeadf-348">IN keyword</span></span>
<span data-ttu-id="eeadf-349">la parola chiave IN Hello può essere utilizzato toocheck se un valore specificato corrisponde a qualsiasi valore in un elenco.</span><span class="sxs-lookup"><span data-stu-id="eeadf-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="eeadf-350">Ad esempio, questa query restituisce tutti i documenti della famiglia dove id hello è uno di "WakefieldFamily" o "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="eeadf-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="eeadf-351">In questo esempio restituisce tutti i documenti in cui è stato hello qualsiasi hello specificato i valori.</span><span class="sxs-lookup"><span data-stu-id="eeadf-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="eeadf-352">Operatori Ternary (?) e Coalesce (??)</span><span class="sxs-lookup"><span data-stu-id="eeadf-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="eeadf-353">gli operatori ternario e Coalesce Hello possono essere utilizzato toobuild espressioni condizionali, simile toopopular linguaggi di programmazione quali c# e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="eeadf-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="eeadf-354">operatore ternario (?) Hello può essere molto utile quando si creano nuove proprietà JSON in hello veloce.</span><span class="sxs-lookup"><span data-stu-id="eeadf-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="eeadf-355">Ad esempio, ora è possibile scrivere i livelli di classe query tooclassify hello in un formato leggibile umano simile per principianti/intermedio/avanzate, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eeadf-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="eeadf-356">È inoltre possibile annidare hello chiamate toohello operatore like in query hello seguente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="eeadf-357">Come con altri operatori di query, se hello proprietà a cui fa riferimento nell'espressione condizionale hello non sono presenti in qualsiasi documento o se i tipi di hello confrontati sono diversi, quindi tali documenti sono esclusi nei risultati della query hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="eeadf-358">Hello operatore Coalesce (?) può essere utilizzato il controllo tooefficiently presenza hello di una proprietà (anche noto come</span><span class="sxs-lookup"><span data-stu-id="eeadf-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="eeadf-359">(definita) in un documento.</span><span class="sxs-lookup"><span data-stu-id="eeadf-359">is defined) in a document.</span></span> <span data-ttu-id="eeadf-360">Questo risulta utile per le query su dati semistrutturati o di tipo misto</span><span class="sxs-lookup"><span data-stu-id="eeadf-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="eeadf-361">Ad esempio, questa query restituisce hello "Cognome" se è presente o hello "Cognome" Se non è presente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="eeadf-362"><a id="EscapingReservedKeywords"></a>Funzione di accesso della proprietà di delimitazione</span><span class="sxs-lookup"><span data-stu-id="eeadf-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="eeadf-363">È inoltre possibile accedere utilizzando l'operatore tra virgolette proprietà hello proprietà `[]`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="eeadf-364">Ad esempio, la sintassi di `SELECT c.grade` and `SELECT c["grade"]` sono equivalenti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="eeadf-365">Questa sintassi è utile quando è necessario tooescape una proprietà che contiene spazi, caratteri speciali, o si verifica hello tooshare stesso nome come una parola chiave SQL o una parola riservata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="eeadf-366"><a id="SelectClause"></a>Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="eeadf-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="eeadf-367">clausola SELECT Hello (**`SELECT <select_list>`**) è obbligatorio e specifica quali valori vengono recuperati dalla query hello, esattamente come in SQL ANSI.</span><span class="sxs-lookup"><span data-stu-id="eeadf-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="eeadf-368">subset di Hello che è stato filtrato su documenti di origine hello vengono passate in fase di proiezione hello, in cui hello specificato vengono recuperati i valori JSON e viene costruito un nuovo oggetto JSON, per ogni input passato su di esso.</span><span class="sxs-lookup"><span data-stu-id="eeadf-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="eeadf-369">Hello di esempio seguente mostra una tipico query SELECT.</span><span class="sxs-lookup"><span data-stu-id="eeadf-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="eeadf-370">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-371">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="eeadf-372">Proprietà annidate</span><span class="sxs-lookup"><span data-stu-id="eeadf-372">Nested properties</span></span>
<span data-ttu-id="eeadf-373">Nell'esempio seguente di hello, ci stiamo proiezione due proprietà annidate `f.address.state` e `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="eeadf-374">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-375">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="eeadf-376">Proiezione supporta anche le espressioni di JSON, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="eeadf-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="eeadf-377">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-378">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="eeadf-379">Diamo un'occhiata ruolo hello di `$1` qui.</span><span class="sxs-lookup"><span data-stu-id="eeadf-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="eeadf-380">Hello `SELECT` clausola deve toocreate un oggetto JSON e poiché non viene fornita alcuna chiave, si utilizzano i nomi delle variabili di argomento implicito a partire da `$1`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="eeadf-381">Ad esempio, questa query restituisce due variabili di argomento implicite, etichettate `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="eeadf-382">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-383">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="eeadf-384">Aliasing</span><span class="sxs-lookup"><span data-stu-id="eeadf-384">Aliasing</span></span>
<span data-ttu-id="eeadf-385">Ora è possibile estendere l'esempio hello precedente con l'aliasing esplicita dei valori.</span><span class="sxs-lookup"><span data-stu-id="eeadf-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="eeadf-386">ESEMPIO hello parola chiave utilizzata per l'alias.</span><span class="sxs-lookup"><span data-stu-id="eeadf-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="eeadf-387">È facoltativo, come illustrato durante la proiezione secondo valore hello come `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="eeadf-388">Nel caso in cui una query contiene due proprietà con hello stesso nome, l'alias devono essere toorename utilizzati uno o entrambi hello proprietà in modo che vengono disambiguati hello proiettato risultato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="eeadf-389">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-390">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="eeadf-391">Espressioni scalari</span><span class="sxs-lookup"><span data-stu-id="eeadf-391">Scalar expressions</span></span>
<span data-ttu-id="eeadf-392">Inoltre tooproperty fa riferimento a, la clausola SELECT hello supporta anche le espressioni scalari, costanti, espressioni aritmetiche, espressioni logiche, ecc. Ad esempio, ecco una semplice query "Hello World".</span><span class="sxs-lookup"><span data-stu-id="eeadf-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="eeadf-393">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="eeadf-394">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="eeadf-395">Di seguito è presentato un esempio più complesso che usa un'espressione scalare.</span><span class="sxs-lookup"><span data-stu-id="eeadf-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="eeadf-396">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="eeadf-397">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="eeadf-398">Nell'esempio seguente di hello, il risultato di hello di espressione scalare hello è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="eeadf-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="eeadf-399">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="eeadf-400">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="eeadf-401">Creazione di oggetti e matrici</span><span class="sxs-lookup"><span data-stu-id="eeadf-401">Object and array creation</span></span>
<span data-ttu-id="eeadf-402">Un'altra funzione fondamentale dell'API SQL di DocumentDB è la creazione di matrici/oggetti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="eeadf-403">Nell'esempio precedente hello, si noti che è stato creato un nuovo oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="eeadf-404">Analogamente, uno inoltre possibile creare matrici come illustrato nell'hello seguono esempi:</span><span class="sxs-lookup"><span data-stu-id="eeadf-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="eeadf-405">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="eeadf-406">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="eeadf-407"><a id="ValueKeyword"></a>Parola chiave VALUE</span><span class="sxs-lookup"><span data-stu-id="eeadf-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="eeadf-408">Hello **valore** (parola chiave) fornisce un valore JSON tooreturn modo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="eeadf-409">Ad esempio, le query hello illustrata di seguito restituisce hello scalare `"Hello World"` anziché `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="eeadf-410">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="eeadf-411">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="eeadf-412">la query seguente Hello restituisce il valore JSON hello senza hello `"address"` etichetta nei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="eeadf-413">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="eeadf-414">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="eeadf-415">Hello esempio estende questo tooshow come valori primitivi tooreturn JSON (livello hello foglia dell'albero di hello JSON).</span><span class="sxs-lookup"><span data-stu-id="eeadf-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="eeadf-416">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="eeadf-417">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="eeadf-418">Operatore *</span><span class="sxs-lookup"><span data-stu-id="eeadf-418">* Operator</span></span>
<span data-ttu-id="eeadf-419">operatore speciale (*) Hello è supportato tooproject hello documento come-è.</span><span class="sxs-lookup"><span data-stu-id="eeadf-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="eeadf-420">Se utilizzato, deve essere hello proiettati solo campo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="eeadf-421">Benché una query come `SELECT * FROM Families f` sia valida, `SELECT VALUE * FROM Families f ` e `SELECT *, f.id FROM Families f ` non lo sono.</span><span class="sxs-lookup"><span data-stu-id="eeadf-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="eeadf-422">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="eeadf-423">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="eeadf-424"><a id="TopKeyword"></a>Operatore TOP</span><span class="sxs-lookup"><span data-stu-id="eeadf-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="eeadf-425">parola chiave TOP Hello può essere utilizzato toolimit hello numero di valori da una query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="eeadf-426">Se TOP viene utilizzato in combinazione con una clausola ORDER BY hello, set di risultati di hello è limitato toohello primo numero N di valori ordinati. in caso contrario, restituisce hello primo numero N di risultati in un ordine non definito.</span><span class="sxs-lookup"><span data-stu-id="eeadf-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="eeadf-427">Come procedura consigliata, in un'istruzione SELECT, utilizzare sempre una clausola ORDER BY con la clausola TOP hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="eeadf-428">Si tratta pertanto hello toopredictably indicano quali righe sono interessate dalla clausola TOP.</span><span class="sxs-lookup"><span data-stu-id="eeadf-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="eeadf-429">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="eeadf-430">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="eeadf-431">È possibile usare TOP con un valore costante (come illustrato in precedenza) o con un valore della variabile usando le query con parametri.</span><span class="sxs-lookup"><span data-stu-id="eeadf-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="eeadf-432">Per altre informazioni dettagliate, vedere le query con parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="eeadf-433"><a id="Aggregates"></a>Funzioni di aggregazione</span><span class="sxs-lookup"><span data-stu-id="eeadf-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="eeadf-434">È inoltre possibile eseguire le aggregazioni in hello `SELECT` clausola.</span><span class="sxs-lookup"><span data-stu-id="eeadf-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="eeadf-435">Le funzioni di aggregazione eseguono un calcolo su un set di valori e restituiscono un singolo valore.</span><span class="sxs-lookup"><span data-stu-id="eeadf-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="eeadf-436">Ad esempio, hello query seguente restituisce il conteggio di hello dei documenti della famiglia insieme hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="eeadf-437">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="eeadf-438">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="eeadf-439">È inoltre possibile restituire valore scalare di hello di hello aggregazione utilizzando hello `VALUE` (parola chiave).</span><span class="sxs-lookup"><span data-stu-id="eeadf-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="eeadf-440">Ad esempio, hello query seguente restituisce il conteggio di hello dei valori come un singolo numero:</span><span class="sxs-lookup"><span data-stu-id="eeadf-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="eeadf-441">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="eeadf-442">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="eeadf-443">È anche possibile eseguire aggregazioni combinate a filtri.</span><span class="sxs-lookup"><span data-stu-id="eeadf-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="eeadf-444">Ad esempio, hello query seguente restituisce il conteggio di hello dei documenti con indirizzo hello in stato di Washington hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="eeadf-445">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="eeadf-446">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="eeadf-447">Hello nella tabella seguente mostra hello elenco di funzioni di aggregazione supportate nell'API di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="eeadf-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="eeadf-448">`SUM`e `AVG` vengono eseguite su valori numerici, mentre `COUNT`, `MIN` e `MAX` possono essere eseguite su numeri, stringhe, valori booleani e valori null.</span><span class="sxs-lookup"><span data-stu-id="eeadf-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="eeadf-449">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="eeadf-449">Usage</span></span> | <span data-ttu-id="eeadf-450">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eeadf-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="eeadf-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="eeadf-451">COUNT</span></span> | <span data-ttu-id="eeadf-452">Restituisce hello numero di elementi in espressione hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="eeadf-453">SUM</span><span class="sxs-lookup"><span data-stu-id="eeadf-453">SUM</span></span>   | <span data-ttu-id="eeadf-454">Restituisce hello somma di tutti i valori hello hello espressione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="eeadf-455">MIN</span><span class="sxs-lookup"><span data-stu-id="eeadf-455">MIN</span></span>   | <span data-ttu-id="eeadf-456">Restituisce hello valore minimo nell'espressione hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="eeadf-457">MAX</span><span class="sxs-lookup"><span data-stu-id="eeadf-457">MAX</span></span>   | <span data-ttu-id="eeadf-458">Restituisce hello valore massimo nell'espressione hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="eeadf-459">MEDIA</span><span class="sxs-lookup"><span data-stu-id="eeadf-459">AVG</span></span>   | <span data-ttu-id="eeadf-460">Restituisce hello Media dei valori hello in espressione hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="eeadf-461">Le aggregazioni possono essere eseguite anche sui risultati di hello di un'iterazione della matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="eeadf-462">Per altre informazioni, vedere [Array Iteration in Queries](#Iteration) (Iterazione della matrice nelle query).</span><span class="sxs-lookup"><span data-stu-id="eeadf-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="eeadf-463">Quando tramite hello Esplora Query del portale di Azure, si noti che le query di aggregazione possono restituire hello risultati aggregati parzialmente su una pagina di query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="eeadf-464">Hello SDK produce un singolo valore cumulativo in tutte le pagine.</span><span class="sxs-lookup"><span data-stu-id="eeadf-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="eeadf-465">Ordine in query di aggregazione tooperform tramite codice, è necessario .NET SDK 1.12.0, .NET Core SDK 1.1.0 o SDK per Java 1.9.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="eeadf-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="eeadf-466"><a id="OrderByClause"></a>Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="eeadf-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="eeadf-467">Come in SQL ANSI, è possibile includere una clausola Order By facoltativa durante l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="eeadf-468">clausola di Hello può includere un parametro facoltativo ASC/DESC toospecify hello ordine degli argomenti in cui devono essere recuperati i risultati.</span><span class="sxs-lookup"><span data-stu-id="eeadf-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="eeadf-469">Ad esempio, ecco una query che recupera i gruppi in ordine di hello residenti il nome di città.</span><span class="sxs-lookup"><span data-stu-id="eeadf-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="eeadf-470">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="eeadf-471">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="eeadf-472">Di seguito è una query che recupera i gruppi nell'ordine della data di creazione, che viene archiviata come un numero che rappresenta di hello valore epoch, ovvero il tempo trascorso dall'1 gennaio 1970, in secondi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="eeadf-473">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="eeadf-474">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="eeadf-475"><a id="Advanced"></a>Concetti avanzati relativi ai database e alle query SQL</span><span class="sxs-lookup"><span data-stu-id="eeadf-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="eeadf-476"><a id="Iteration"></a>Iterazione</span><span class="sxs-lookup"><span data-stu-id="eeadf-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="eeadf-477">È stato aggiunto un nuovo costrutto di tramite hello **IN** parola chiave DocumentDB API tooprovide supporto tecnico di SQL per scorrere le matrici JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="eeadf-478">origine FROM Hello fornisce supporto per l'iterazione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="eeadf-479">Iniziamo con hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="eeadf-479">Let's start with hello following example:</span></span>

<span data-ttu-id="eeadf-480">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="eeadf-481">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="eeadf-482">Ora diamo un'occhiata a un'altra query che esegue l'iterazione figlio nella raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="eeadf-483">Si noti la differenza hello nella matrice di output di hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="eeadf-484">Questo esempio suddivide `children` e appiattisce risultati hello in una matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="eeadf-485">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="eeadf-486">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="eeadf-487">Può essere ulteriormente utilizzati toofilter in ogni singola voce della matrice di hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="eeadf-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="eeadf-488">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="eeadf-489">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="eeadf-490">È anche possibile eseguire l'aggregazione per il risultato di hello di iterazione di matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="eeadf-491">Ad esempio, hello nella query seguente conta hello figli tra tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="eeadf-492">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="eeadf-493">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="eeadf-494"><a id="Joins"></a>Join</span><span class="sxs-lookup"><span data-stu-id="eeadf-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="eeadf-495">In un database relazionale, è importante hello necessità toojoin tra le tabelle.</span><span class="sxs-lookup"><span data-stu-id="eeadf-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="eeadf-496">Di hello logico toodesigning corollario normalizzato schemi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="eeadf-497">Toothis contrarie, l'API DocumentDB riguarda il modello di dati denormalizzati hello di documenti privi di schema.</span><span class="sxs-lookup"><span data-stu-id="eeadf-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="eeadf-498">Si tratta hello equivalente logico di un "self-join".</span><span class="sxs-lookup"><span data-stu-id="eeadf-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="eeadf-499">sintassi di Hello che supporta la lingua di hello è JOIN JOIN < from_source2 > di < from_source1 >... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="eeadf-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="eeadf-500">In generale, restituisce un set di tuple **N** (tupla con valori **N**).</span><span class="sxs-lookup"><span data-stu-id="eeadf-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="eeadf-501">Ogni tupla ha valori prodotti dall'iterazione di tutti gli alias della raccolta sui rispettivi set.</span><span class="sxs-lookup"><span data-stu-id="eeadf-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="eeadf-502">In altre parole, questo è un prodotto incrociato completo dei set di hello che fanno parte di join hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="eeadf-503">Hello esempi seguenti viene illustrato il funzionamento clausola JOIN hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="eeadf-504">Nell'esempio seguente di hello, hello risulta vuota poiché hello prodotto incrociato di ogni documento di origine e un set vuoto è vuoto.</span><span class="sxs-lookup"><span data-stu-id="eeadf-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="eeadf-505">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="eeadf-506">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="eeadf-507">Nell'esempio seguente di hello, join hello è compreso tra la radice del documento hello e hello `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="eeadf-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="eeadf-508">È un prodotto incrociato tra due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="eeadf-509">fatti Hello che gli elementi figlio è una matrice non sono efficaci per hello JOIN poiché ci stiamo gestiscono un solo nodo radice è una matrice di figli hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="eeadf-510">Pertanto il risultato di hello contiene solo due risultati, poiché il prodotto incrociato di tutti i documenti con matrice hello hello produce esattamente un solo documento.</span><span class="sxs-lookup"><span data-stu-id="eeadf-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="eeadf-511">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="eeadf-512">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="eeadf-513">Hello di esempio seguente viene illustrato un join di più tradizionale:</span><span class="sxs-lookup"><span data-stu-id="eeadf-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="eeadf-514">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="eeadf-515">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="eeadf-516">Hello in primo luogo toonote è tale hello `from_source` di hello **JOIN** clausola è un iteratore.</span><span class="sxs-lookup"><span data-stu-id="eeadf-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="eeadf-517">In tal caso, il flusso di hello in questo caso è come segue:</span><span class="sxs-lookup"><span data-stu-id="eeadf-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="eeadf-518">Espandere ogni elemento figlio **c** nella matrice hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="eeadf-519">Applicare un prodotto incrociato con la radice del documento hello hello **f** con ogni elemento figlio **c** che è stata semplificata nel primo passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="eeadf-520">Infine, progetto oggetto radice hello **f** solo proprietà name.</span><span class="sxs-lookup"><span data-stu-id="eeadf-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="eeadf-521">primo documento Hello (`AndersenFamily`) contiene un solo elemento figlio, in modo hello set di risultati contiene solo un documento di toothis corrispondente dell'oggetto singolo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="eeadf-522">secondo documento Hello (`WakefieldFamily`) contiene due elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="eeadf-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="eeadf-523">In tal caso, hello prodotto incrociato produce un oggetto separato per ogni elemento figlio, determinando in tal modo due oggetti, uno per ogni documento di toothis figlio corrispondente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="eeadf-524">radice Hello campi in entrambi questi documenti sono hello stesso, come previsto in un prodotto incrociato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="eeadf-525">Hello reale utilità hello JOIN è tooform tuple dal prodotto incrociato hello in una forma che altrimenti tooproject difficile.</span><span class="sxs-lookup"><span data-stu-id="eeadf-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="eeadf-526">Inoltre, come si può vedere nel seguente esempio hello, è possibile filtrare in combinazione hello di una tupla hello degli che consente l'utente ha scelto una condizione soddisfatta da tuple hello complessiva.</span><span class="sxs-lookup"><span data-stu-id="eeadf-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="eeadf-527">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="eeadf-528">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="eeadf-529">In questo esempio è un'estensione naturale della hello sopra riportato, esegue un join double.</span><span class="sxs-lookup"><span data-stu-id="eeadf-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="eeadf-530">In tal caso, hello prodotto incrociato possono essere visualizzato come hello pseudo-codice seguente:</span><span class="sxs-lookup"><span data-stu-id="eeadf-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="eeadf-531">`AndersenFamily` ha un figlio che ha un animale domestico.</span><span class="sxs-lookup"><span data-stu-id="eeadf-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="eeadf-532">In tal caso, hello prodotto incrociato restituisce una riga (1\*1\*1) da questa famiglia.</span><span class="sxs-lookup"><span data-stu-id="eeadf-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="eeadf-533">Tuttavia, la famiglia WakefieldFamily ha due figli, ma un solo figlio, "Jesse", ha animali domestici.</span><span class="sxs-lookup"><span data-stu-id="eeadf-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="eeadf-534">Jesse ha però due animali domestici.</span><span class="sxs-lookup"><span data-stu-id="eeadf-534">Jesse has two pets though.</span></span> <span data-ttu-id="eeadf-535">Di conseguenza hello prodotto incrociato restituisce 1\*1\*2 = 2 righe da questa famiglia.</span><span class="sxs-lookup"><span data-stu-id="eeadf-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="eeadf-536">Nell'esempio riportato di seguito hello, è un ulteriore filtro su `pet`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="eeadf-537">Consente di escludere tutte le tuple hello in cui non è "Shadow" hello pet nome.</span><span class="sxs-lookup"><span data-stu-id="eeadf-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="eeadf-538">Si noti che è in grado di toobuild tuple da matrici, filtro in uno qualsiasi degli elementi di hello di tupla hello e qualsiasi combinazione di elementi di hello del progetto.</span><span class="sxs-lookup"><span data-stu-id="eeadf-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="eeadf-539">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="eeadf-540">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="eeadf-541"><a id="JavaScriptIntegration"></a>Integrazione JavaScript</span><span class="sxs-lookup"><span data-stu-id="eeadf-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="eeadf-542">DB Cosmos Azure fornisce un modello di programmazione per l'esecuzione di logica dell'applicazione basata su JavaScript direttamente nelle raccolte di hello in termini di stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="eeadf-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="eeadf-543">Ciò consente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="eeadf-543">This allows for both:</span></span>

* <span data-ttu-id="eeadf-544">Operazioni CRUD transazionale di possibilità toodo ad alte prestazioni e le query su documenti in una raccolta in virtù di integrazione hello del runtime JavaScript direttamente nel motore di database hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="eeadf-545">Modellazione naturale del flusso di controllo, definizione dell'ambito delle variabili e assegnazione e integrazione di primitivi di gestione delle eccezioni con transazioni di database.</span><span class="sxs-lookup"><span data-stu-id="eeadf-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="eeadf-546">Per ulteriori informazioni sul supporto di Azure Cosmos DB per l'integrazione con JavaScript, consultare la documentazione di toohello JavaScript sul lato server programmabilità.</span><span class="sxs-lookup"><span data-stu-id="eeadf-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="eeadf-547"><a id="UserDefinedFunctions"></a>Funzioni definite dall'utente (UDF)</span><span class="sxs-lookup"><span data-stu-id="eeadf-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="eeadf-548">Oltre ai tipi di hello già definiti in questo articolo, SQL API DocumentDB fornisce il supporto per utente definite funzioni (funzione definita dall'utente).</span><span class="sxs-lookup"><span data-stu-id="eeadf-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="eeadf-549">In particolare, funzioni definite dall'utente scalari sono supportate in cui gli sviluppatori di hello possono passare zero o più argomenti e restituire un risultato singolo argomento.</span><span class="sxs-lookup"><span data-stu-id="eeadf-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="eeadf-550">Verrà quindi eseguito un controllo per verificare che ciascuno di questi argomenti sia un valore JSON legale.</span><span class="sxs-lookup"><span data-stu-id="eeadf-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="eeadf-551">la sintassi SQL API DocumentDB Hello viene estesa toosupport logica dell'applicazione personalizzata utilizzando le funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="eeadf-552">Le UDF possono essere registrate con l'API di DocumentDB ed è quindi possibile fare loro riferimento come parte di una query SQL.</span><span class="sxs-lookup"><span data-stu-id="eeadf-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="eeadf-553">In effetti, funzioni definite dall'utente sono exquisitely hello progettato toobe richiamata da una query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="eeadf-554">Come scelta toothis corollario, funzioni definite dall'utente non dispongono di accesso toohello contesto oggetto cui hello altre JavaScript dispongono di tipi (stored procedure e trigger).</span><span class="sxs-lookup"><span data-stu-id="eeadf-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="eeadf-555">Poiché le query vengono eseguite in sola lettura, è possibile eseguirle sulle repliche primarie o secondarie.</span><span class="sxs-lookup"><span data-stu-id="eeadf-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="eeadf-556">Pertanto, funzioni definite dall'utente sono progettati toorun nelle repliche secondarie, a differenza di altri tipi di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="eeadf-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="eeadf-557">Di seguito è riportato un esempio di come una funzione definita dall'utente possono essere registrati nel database DB Cosmos hello, in particolare in una raccolta documenti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="eeadf-558">esempio Hello crea una funzione definita dall'utente il cui nome è `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="eeadf-559">Accetta due valori stringa JSON `input` e `pattern` e controlla se le corrispondenze prima hello hello criterio specificato in hello secondo funzione JavaScript string.match().</span><span class="sxs-lookup"><span data-stu-id="eeadf-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="eeadf-560">È ora possibile usare questa UDF in una query in una proiezione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="eeadf-561">Funzioni definite dall'utente deve essere qualificato con prefisso distinzione maiuscole/minuscole hello "definita dall'utente."</span><span class="sxs-lookup"><span data-stu-id="eeadf-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="eeadf-562">quando chiamate dall'interno delle query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="eeadf-563">Precedente too3/17/2015 Cosmos DB supportato chiamate di funzione definita dall'utente senza hello "definita dall'utente."</span><span class="sxs-lookup"><span data-stu-id="eeadf-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="eeadf-564">come SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="eeadf-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="eeadf-565">Questo modello di chiamata è stato deprecato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="eeadf-566">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="eeadf-567">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="eeadf-568">funzione definita dall'utente Hello consente anche all'interno di un filtro come illustrato nell'esempio hello riportato di seguito, anche qualificato con hello "definita dall'utente."</span><span class="sxs-lookup"><span data-stu-id="eeadf-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="eeadf-569">prefisso:</span><span class="sxs-lookup"><span data-stu-id="eeadf-569">prefix:</span></span>

<span data-ttu-id="eeadf-570">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="eeadf-571">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="eeadf-572">In sostanza, le UDF sono espressioni scalari valide che è possibile usare sia nelle proiezioni sia nei filtri.</span><span class="sxs-lookup"><span data-stu-id="eeadf-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="eeadf-573">tooexpand alimentato hello di funzioni definite dall'utente, si esaminerà un altro esempio con la logica condizionale:</span><span class="sxs-lookup"><span data-stu-id="eeadf-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="eeadf-574">Di seguito è riportato un esempio che esercizi hello funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="eeadf-575">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="eeadf-576">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="eeadf-577">Come hello showcase esempi precedenti, funzioni definite dall'utente integrarlo power hello del linguaggio JavaScript hello SQL API DocumentDB tooprovide una ricca interfaccia programmabile toodo procedurale, condizionale logica complessa con l'aiuto di hello del runtime JavaScript incorporato funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eeadf-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="eeadf-578">SQL API DocumentDB fornisce argomenti di hello toohello funzioni definite dall'utente per ogni documento nell'origine hello fase hello corrente (clausola WHERE o clausola SELECT) di elaborazione hello funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="eeadf-579">Hello risultato viene incorporato hello generale della pipeline di esecuzione senza problemi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="eeadf-580">Se le proprietà di hello parametri di funzione definita dall'utente hello tooby cui viene fatto riferimento non sono disponibili in hello valore JSON, hello parametro viene considerato come non definito e pertanto hello viene ignorata completamente la chiamata di funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="eeadf-581">Allo stesso modo se il risultato di hello della funzione definita dall'utente hello è definito, non è incluso nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="eeadf-582">In sintesi, funzioni definite dall'utente sono logica di business complessa toodo validi strumenti come parte di query hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="eeadf-583">Valutazione degli operatori</span><span class="sxs-lookup"><span data-stu-id="eeadf-583">Operator evaluation</span></span>
<span data-ttu-id="eeadf-584">In virtù di hello di essere un database, JSON COSMOS DB, disegna parallels con operatori JavaScript e la semantica di valutazione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="eeadf-585">Mentre DB Cosmos tenta la semantica JavaScript toopreserve in termini di supporto JSON, valutazione operazione hello devia in alcuni casi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="eeadf-586">In SQL API DocumentDB, a differenza di SQL tradizionale, hello tipi di valori, spesso non noti fino a quando i valori hello vengono recuperati dal database.</span><span class="sxs-lookup"><span data-stu-id="eeadf-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="eeadf-587">In ordine tooefficiently eseguire query, la maggior parte degli operatori hello hanno requisiti di tipo strict.</span><span class="sxs-lookup"><span data-stu-id="eeadf-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="eeadf-588">L'API SQL di DocumentDB non esegue conversioni implicite, a differenza di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="eeadf-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="eeadf-589">Ad esempio, una query come `SELECT * FROM Person p WHERE p.Age = 21` corrisponde a documenti che contengono una proprietà Age il cui valore è 21.</span><span class="sxs-lookup"><span data-stu-id="eeadf-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="eeadf-590">Qualsiasi altro documento la cui proprietà Age corrisponde alla stringa "21", o ad altre possibili variazioni come "021", "21.0", "0021", "00021" e così via, non verrà trovato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="eeadf-591">Si tratta invece toohello JavaScript in cui i valori stringa hello sono toonumbers eseguito in modo implicito il cast (basato su operatore, ad esempio: = =).</span><span class="sxs-lookup"><span data-stu-id="eeadf-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="eeadf-592">Questa scelta è fondamentale per la ricerca di indici corrispondenti nell'API SQL di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="eeadf-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="eeadf-593">Query SQL con parametri</span><span class="sxs-lookup"><span data-stu-id="eeadf-593">Parameterized SQL queries</span></span>
<span data-ttu-id="eeadf-594">COSMOS DB supporta le query con parametri espressi con hello familiare notazione @.</span><span class="sxs-lookup"><span data-stu-id="eeadf-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="eeadf-595">SQL con parametri fornisce solide capacità di gestione ed escape dell'input utente, evitando l'esposizione accidentale di dati mediante attacchi SQL injection.</span><span class="sxs-lookup"><span data-stu-id="eeadf-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="eeadf-596">Ad esempio, è possibile scrivere una query che accetta come parametri il cognome e lo stato di residenza e quindi eseguirla per diversi valori di cognome e stato di residenza in base all'input dell'utente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="eeadf-597">Questa richiesta può quindi essere inviata tooCosmos DB come una query con parametri di JSON, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eeadf-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="eeadf-598">Hello argomento tooTOP può essere impostato utilizzando le query con parametri, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eeadf-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="eeadf-599">I valori dei parametri possono essere qualsiasi valore JSON valido (stringhe, numeri, valori booleani, valori null, persino matrici o valori JSON annidati).</span><span class="sxs-lookup"><span data-stu-id="eeadf-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="eeadf-600">Inoltre, dato che Cosmos DB è senza schema, i parametri non vengono convalidati rispetto a qualsiasi tipo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="eeadf-601"><a id="BuiltinFunctions"></a>Funzioni predefinite</span><span class="sxs-lookup"><span data-stu-id="eeadf-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="eeadf-602">Cosmos DB supporta anche una serie di funzioni predefinite per le operazioni comuni, che possono essere usate all'interno di query come le funzioni definite dall'utente (UDF).</span><span class="sxs-lookup"><span data-stu-id="eeadf-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="eeadf-603">Gruppo di funzioni</span><span class="sxs-lookup"><span data-stu-id="eeadf-603">Function group</span></span>          | <span data-ttu-id="eeadf-604">Operazioni</span><span class="sxs-lookup"><span data-stu-id="eeadf-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="eeadf-605">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="eeadf-605">Mathematical functions</span></span>  | <span data-ttu-id="eeadf-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, gradi, PI, radianti, SIN e TAN</span><span class="sxs-lookup"><span data-stu-id="eeadf-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="eeadf-607">Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="eeadf-607">Type checking functions</span></span> | <span data-ttu-id="eeadf-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="eeadf-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="eeadf-609">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="eeadf-609">String functions</span></span>        | <span data-ttu-id="eeadf-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, sinistra, lunghezza, inferiore, LTRIM, REPLACE, replica, inversa, destra, RTRIM, STARTSWITH, SUBSTRING e superiore</span><span class="sxs-lookup"><span data-stu-id="eeadf-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="eeadf-611">Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="eeadf-611">Array functions</span></span>         | <span data-ttu-id="eeadf-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH e ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="eeadf-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="eeadf-613">Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="eeadf-613">Spatial functions</span></span>       | <span data-ttu-id="eeadf-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID e ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="eeadf-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="eeadf-615">Se attualmente si utilizza una funzione definita dall'utente (UDF) per il quale è ora disponibile una funzione predefinita, è necessario usare la funzione incorporata corrispondente di hello come saranno toobe toorun di più veloce e più efficiente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="eeadf-616">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="eeadf-616">Mathematical functions</span></span>
<span data-ttu-id="eeadf-617">Hello funzioni matematiche eseguono un calcolo, in base ai valori di input forniti come argomenti e restituiscono un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="eeadf-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="eeadf-618">Di seguito è riportata una tabella delle funzioni matematiche predefinite supportate.</span><span class="sxs-lookup"><span data-stu-id="eeadf-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="eeadf-619">Uso</span><span class="sxs-lookup"><span data-stu-id="eeadf-619">Usage</span></span> | <span data-ttu-id="eeadf-620">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eeadf-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="eeadf-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="eeadf-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="eeadf-622">Restituisce hello assoluto (positivo) il valore di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="eeadf-624">Restituisce hello più piccolo valore integer maggiore di o uguale a, hello espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="eeadf-626">Restituisce l'intero più grande hello minore o uguale toohello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="eeadf-628">Esponente hello restituisce di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="eeadf-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="eeadf-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="eeadf-630">Logaritmo naturale di hello restituisce di hello specificato espressione numerica o logaritmo hello utilizzando hello specificato base</span><span class="sxs-lookup"><span data-stu-id="eeadf-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="eeadf-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="eeadf-632">Restituisce valori logaritmico hello in base 10 di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="eeadf-634">Restituisce un valore numerico, il valore intero più vicino di toohello arrotondato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="eeadf-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="eeadf-636">Restituisce un valore numerico, il valore intero più vicino di toohello troncato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="eeadf-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="eeadf-638">Radice quadrata di hello restituisce di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="eeadf-640">Hello restituisce quadrato di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="eeadf-642">Restituisce hello potenza hello specificato valore toohello espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="eeadf-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="eeadf-644">Espressione numerica restituisce hello sign valore (-1, 0, 1) di hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="eeadf-646">Angolo di hello restituisce, in radianti, il cui coseno è hello espressione numerica specificata; denominato anche arcocoseno.</span><span class="sxs-lookup"><span data-stu-id="eeadf-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="eeadf-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="eeadf-648">Angolo di hello restituisce, in radianti, il cui seno è hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="eeadf-649">Detta anche arcoseno.</span><span class="sxs-lookup"><span data-stu-id="eeadf-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="eeadf-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="eeadf-651">Angolo di hello restituisce, in radianti, la cui tangente è hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="eeadf-652">Detta anche arcotangente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="eeadf-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="eeadf-654">Restituisce hello angolo, espresso in radianti, tra l'asse x positivo hello e raggio hello dal punto di toohello origine hello (y, x), dove x e y sono valori hello di hello due espressioni float specificate.</span><span class="sxs-lookup"><span data-stu-id="eeadf-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="eeadf-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="eeadf-656">Restituisce hello coseno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="eeadf-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="eeadf-658">Restituisce hello cotangente trigonometrica hello specificato angolo, espresso in radianti, in hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="eeadf-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="eeadf-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="eeadf-660">Restituisce hello angolo corrispondente in gradi di un angolo specificato espresso in radianti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="eeadf-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="eeadf-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="eeadf-662">Restituisce hello valore costante di pi greco.</span><span class="sxs-lookup"><span data-stu-id="eeadf-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="eeadf-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="eeadf-664">Restituisce radianti quando viene immessa un'espressione numerica, espresso in gradi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="eeadf-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="eeadf-666">Restituisce hello seno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="eeadf-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="eeadf-668">Tangente di hello restituisce dell'espressione di input hello, in hello espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="eeadf-669">Ad esempio, è ora possibile eseguire query hello seguente:</span><span class="sxs-lookup"><span data-stu-id="eeadf-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="eeadf-670">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="eeadf-671">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-671">**Results**</span></span>

    [4]

<span data-ttu-id="eeadf-672">Hello differenza principale tooANSI funzioni rispetto Cosmos DB SQL è che si trovano toowork progettato correttamente con i dati dello schema senza schema e misto.</span><span class="sxs-lookup"><span data-stu-id="eeadf-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="eeadf-673">Ad esempio, se si dispone di un documento in cui la proprietà di dimensione hello mancante, o con un valore non numerico come "sconosciuto", quindi il documento hello viene ignorato, anziché restituire un errore.</span><span class="sxs-lookup"><span data-stu-id="eeadf-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="eeadf-674">Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="eeadf-674">Type checking functions</span></span>
<span data-ttu-id="eeadf-675">funzioni di controllo di tipo Hello consentono di tipo hello toocheck di un'espressione all'interno di query SQL.</span><span class="sxs-lookup"><span data-stu-id="eeadf-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="eeadf-676">Tipo di funzioni di controllo possono essere utilizzato tipo hello toodetermine delle proprietà all'interno di documenti in tempo reale di hello quando è sconosciuto o variabile.</span><span class="sxs-lookup"><span data-stu-id="eeadf-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="eeadf-677">Di seguito è riportata una tabella di funzioni predefinite di controllo del tipo supportate.</span><span class="sxs-lookup"><span data-stu-id="eeadf-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="eeadf-678"><strong>Utilizzo</strong></span><span class="sxs-lookup"><span data-stu-id="eeadf-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="eeadf-679"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="eeadf-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-681">Restituisce un valore booleano che indica se il tipo di hello del valore di hello è una matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-683">Restituisce un valore booleano che indica se il tipo di hello del valore di hello è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="eeadf-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-685">Restituisce un valore booleano che indica se il tipo di hello del valore di hello è null.</span><span class="sxs-lookup"><span data-stu-id="eeadf-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-687">Restituisce un valore booleano che indica se il tipo di hello del valore di hello è un numero.</span><span class="sxs-lookup"><span data-stu-id="eeadf-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-689">Restituisce un valore booleano che indica se il tipo di hello del valore di hello è un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-691">Restituisce un valore booleano che indica se il tipo di hello del valore di hello è una stringa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-693">Restituisce un valore booleano che indica se la proprietà hello è stata assegnata un valore.</span><span class="sxs-lookup"><span data-stu-id="eeadf-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="eeadf-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="eeadf-695">Restituisce un valore booleano che indica se il tipo di hello del valore di hello è una stringa, numero, booleano o null.</span><span class="sxs-lookup"><span data-stu-id="eeadf-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="eeadf-696">Utilizzo di queste funzioni, è possibile eseguire query hello seguente:</span><span class="sxs-lookup"><span data-stu-id="eeadf-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="eeadf-697">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="eeadf-698">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="eeadf-699">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="eeadf-699">String functions</span></span>
<span data-ttu-id="eeadf-700">Hello funzioni scalari seguenti eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="eeadf-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="eeadf-701">Ecco una tabella di funzioni per stringhe:</span><span class="sxs-lookup"><span data-stu-id="eeadf-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="eeadf-702">Uso</span><span class="sxs-lookup"><span data-stu-id="eeadf-702">Usage</span></span> | <span data-ttu-id="eeadf-703">Description</span><span class="sxs-lookup"><span data-stu-id="eeadf-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="eeadf-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="eeadf-705">Espressione di stringa specificata di hello restituisce il numero di caratteri di hello</span><span class="sxs-lookup"><span data-stu-id="eeadf-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="eeadf-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="eeadf-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="eeadf-707">Restituisce una stringa che rappresenta il risultato di hello del concatenamento di due o più valori di stringa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="eeadf-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="eeadf-709">Restituisce parte di un'espressione stringa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="eeadf-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="eeadf-711">Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo</span><span class="sxs-lookup"><span data-stu-id="eeadf-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="eeadf-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="eeadf-713">Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo</span><span class="sxs-lookup"><span data-stu-id="eeadf-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="eeadf-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="eeadf-715">Restituisce un valore booleano che indica se prima espressione di stringa hello contiene hello secondo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="eeadf-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="eeadf-717">Restituisce hello a partire dalla posizione della prima occorrenza di hello della seconda espressione stringa hello all'hello prima espressione stringa specificata oppure -1 se la stringa hello non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="eeadf-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="eeadf-719">Restituisce la parte sinistra di una stringa di hello con hello specificato numero di caratteri.</span><span class="sxs-lookup"><span data-stu-id="eeadf-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="eeadf-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="eeadf-721">Hello restituisce parte destra di una stringa con hello numero specificato di caratteri.</span><span class="sxs-lookup"><span data-stu-id="eeadf-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="eeadf-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="eeadf-723">Restituisce un'espressione stringa dopo aver rimosso gli spazi vuoti iniziali.</span><span class="sxs-lookup"><span data-stu-id="eeadf-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="eeadf-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="eeadf-725">Restituisce un'espressione stringa dopo la rimozione di tutti gli spazi vuoti finali.</span><span class="sxs-lookup"><span data-stu-id="eeadf-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="eeadf-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="eeadf-727">Restituisce un'espressione stringa dopo aver convertito i caratteri maiuscoli in caratteri toolowercase di dati.</span><span class="sxs-lookup"><span data-stu-id="eeadf-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="eeadf-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="eeadf-729">Restituisce un'espressione stringa dopo la conversione toouppercase di dati carattere minuscolo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="eeadf-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="eeadf-731">Sostituisce tutte le occorrenze di un valore stringa specificato con un altro valore stringa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="eeadf-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="eeadf-733">Ripete un valore stringa in un numero di volte specificato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="eeadf-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="eeadf-735">Restituisce l'inverso di hello di un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="eeadf-736">Utilizzo di queste funzioni, è possibile eseguire query hello seguente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="eeadf-737">Ad esempio, si può restituire il nome della famiglia di hello in lettere maiuscole come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="eeadf-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="eeadf-738">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="eeadf-739">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="eeadf-740">In alternativa, è possibile concatenare stringhe come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="eeadf-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="eeadf-741">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="eeadf-742">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="eeadf-743">Funzioni di stringa possono essere utilizzate anche in hello in risultati toofilter clausola, come nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="eeadf-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="eeadf-744">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="eeadf-745">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="eeadf-746">Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="eeadf-746">Array functions</span></span>
<span data-ttu-id="eeadf-747">Hello funzioni scalari seguenti esegue un'operazione su un valore di input di matrice e restituito numerico, valore booleano o di matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="eeadf-748">La tabella seguente include funzioni di matrice predefinite:</span><span class="sxs-lookup"><span data-stu-id="eeadf-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="eeadf-749">Uso</span><span class="sxs-lookup"><span data-stu-id="eeadf-749">Usage</span></span> | <span data-ttu-id="eeadf-750">Description</span><span class="sxs-lookup"><span data-stu-id="eeadf-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="eeadf-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="eeadf-752">Restituisce il numero di elementi di hello hello specificata espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="eeadf-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="eeadf-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="eeadf-754">Restituisce una matrice che rappresenta il risultato di hello della concatenazione di due o più valori della matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="eeadf-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="eeadf-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="eeadf-756">Restituisce un valore booleano che indica se la matrice hello contiene hello valore specificato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="eeadf-757">Può specificare se la corrispondenza hello è completo o parziale.</span><span class="sxs-lookup"><span data-stu-id="eeadf-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="eeadf-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="eeadf-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="eeadf-759">Restituisce parte di un'espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="eeadf-760">Funzioni di matrice possono essere matrici toomanipulate utilizzati all'interno di JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="eeadf-761">Ad esempio, ecco una query che restituisce tutti i documenti in cui uno degli elementi padre hello è "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="eeadf-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="eeadf-762">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="eeadf-763">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="eeadf-764">È possibile specificare un frammento parziale per gli elementi corrispondenti all'interno della matrice hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="eeadf-765">Hello nella query seguente consente di trovare tutti gli elementi padre con hello `givenName` di `Robin`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="eeadf-766">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="eeadf-767">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="eeadf-768">Di seguito è riportato un altro che usa ARRAY_LENGTH tooget hello numero di elementi figlio per ogni famiglia.</span><span class="sxs-lookup"><span data-stu-id="eeadf-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="eeadf-769">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="eeadf-770">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="eeadf-771">Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="eeadf-771">Spatial functions</span></span>
<span data-ttu-id="eeadf-772">COSMOS DB supporta hello seguendo le funzioni predefinite di Open Geospatial Consortium (OGC) per l'esecuzione di query geospaziale.</span><span class="sxs-lookup"><span data-stu-id="eeadf-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="eeadf-773"><strong>Utilizzo</strong></span><span class="sxs-lookup"><span data-stu-id="eeadf-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="eeadf-774"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="eeadf-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="eeadf-776">Restituisce la distanza hello tra espressioni di hello due LineString, Polygon o punto GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="eeadf-778">Restituisce un'espressione booleana che indica se hello prima GeoJSON oggetto (punto, poligono o LineString) all'interno di hello secondo GeoJSON oggetto (punto, poligono o LineString).</span><span class="sxs-lookup"><span data-stu-id="eeadf-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="eeadf-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="eeadf-780">Restituisce un'espressione booleana che indica se si intersecano hello due GeoJSON oggetti specificati (punto, poligono o LineString).</span><span class="sxs-lookup"><span data-stu-id="eeadf-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="eeadf-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="eeadf-782">Restituisce un valore booleano che indica se hello LineString, Polygon o punto GeoJSON espressione è valida.</span><span class="sxs-lookup"><span data-stu-id="eeadf-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="eeadf-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="eeadf-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="eeadf-784">Restituisce un valore JSON che contiene un valore booleano se hello specificato LineString, Polygon o punto GeoJSON espressione sia valido e se non è valido, è inoltre hello motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="eeadf-785">Le funzioni spaziali possono essere utilizzati tooperform prossimità query sui dati spaziali.</span><span class="sxs-lookup"><span data-stu-id="eeadf-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="eeadf-786">Ad esempio, ecco una query che restituisce che tutti i prodotti della famiglia di documenti che è all'interno di 30 km di hello posizione specificata usando hello ST_DISTANCE funzione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eeadf-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="eeadf-787">**Query**</span><span class="sxs-lookup"><span data-stu-id="eeadf-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="eeadf-788">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="eeadf-789">Per informazioni dettagliate sul supporto geospaziale in Cosmos DB, vedere [Uso dei dati geospaziali in Azure Cosmos DB](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="eeadf-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="eeadf-790">Che esegue il wrapping di funzioni spaziali e hello sintassi SQL per Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eeadf-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="eeadf-791">Ora esaminata in modo LINQ query funzioni e le relative modalità di interazione con la sintassi di hello abbiamo visto finora.</span><span class="sxs-lookup"><span data-stu-id="eeadf-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="eeadf-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="eeadf-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="eeadf-793">LINQ è un modello di programmazione .NET che esprime il calcolo come query su flussi di oggetti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="eeadf-794">COSMOS DB fornisce un toointerface libreria lato client con LINQ facilitando la conversione tra JSON e gli oggetti .NET e un mapping da un subset di LINQ query query tooCosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eeadf-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="eeadf-795">immagine Hello seguente mostra l'architettura hello di supportare le query LINQ tramite DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eeadf-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="eeadf-796">Client DB Cosmos di hello gli sviluppatori possono creare un **IQueryable** che direttamente le query hello Cosmos DB provider di query, che quindi converte query LINQ hello in una query Cosmos DB dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="eeadf-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="eeadf-797">query Hello viene quindi passato toohello tooretrieve server DB Cosmos un set di risultati in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="eeadf-798">Hello ha restituito i risultati vengono deserializzati in un flusso di oggetti .NET sul lato client hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![Architettura di supporto delle query LINQ usando API DocumentDB - Sintassi SQL, linguaggio di query JSON, concetti relativi ai database e query SQL][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="eeadf-800">Mapping .NET e JSON</span><span class="sxs-lookup"><span data-stu-id="eeadf-800">.NET and JSON mapping</span></span>
<span data-ttu-id="eeadf-801">mapping di Hello tra gli oggetti .NET e documenti JSON è naturale, viene eseguito il mapping di ogni campo del membro dati oggetto JSON tooa, dove il nome di campo hello è stato eseguito il mapping di parte di "chiave" toohello dell'oggetto hello e parte "value" hello è parte del valore toohello in modo ricorsivo il mapping dell'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="eeadf-802">Prendere in considerazione hello di esempio seguente: hello famiglia l'oggetto creato è documento JSON toohello mappato come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eeadf-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="eeadf-803">E viceversa, documento JSON hello oggetto .NET tooa indietro mappato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="eeadf-804">**Classe C#**</span><span class="sxs-lookup"><span data-stu-id="eeadf-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="eeadf-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="eeadf-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a><span data-ttu-id="eeadf-806">Conversione tooSQL LINQ</span><span class="sxs-lookup"><span data-stu-id="eeadf-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="eeadf-807">provider di query Cosmos DB Hello esegue il mapping di un lavoro richiesto più di una query LINQ in una query SQL del database Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eeadf-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="eeadf-808">In hello seguente descrizione, si presuppone il lettore di hello ha una conoscenza di base di LINQ.</span><span class="sxs-lookup"><span data-stu-id="eeadf-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="eeadf-809">In primo luogo, per il sistema di tipi di hello, sostegno tutti JSON i tipi primitivi, tipi numerici, boolean, string e null.</span><span class="sxs-lookup"><span data-stu-id="eeadf-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="eeadf-810">Sono supportati solo questi tipi JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-810">Only these JSON types are supported.</span></span> <span data-ttu-id="eeadf-811">Hello seguenti espressioni scalari è supportata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="eeadf-812">Valori costanti – tra valori costanti di tipi di dati primitivi hello in fase di hello hello query viene valutata.</span><span class="sxs-lookup"><span data-stu-id="eeadf-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="eeadf-813">Espressioni di indice di matrice delle proprietà-queste espressioni fanno riferimento toohello proprietà di un oggetto o un elemento di matrice.</span><span class="sxs-lookup"><span data-stu-id="eeadf-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="eeadf-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n è una variabile di tipo int</span><span class="sxs-lookup"><span data-stu-id="eeadf-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="eeadf-815">Espressioni aritmetiche: includono espressioni aritmetiche comuni su valori numerici e booleani.</span><span class="sxs-lookup"><span data-stu-id="eeadf-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="eeadf-816">Per l'elenco completo di hello, consultare toohello specifica di SQL.</span><span class="sxs-lookup"><span data-stu-id="eeadf-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="eeadf-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="eeadf-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="eeadf-818">Espressione di confronto stringa - tra cui il confronto di un valore di stringa costante toosome valore stringa.</span><span class="sxs-lookup"><span data-stu-id="eeadf-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="eeadf-819">mother.familyName == "Smith";    child.givenName == s; //s è una variabile di stringa</span><span class="sxs-lookup"><span data-stu-id="eeadf-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="eeadf-820">Espressione di creazione oggetto/matrice: restituisce un oggetto di tipo valore composito o tipo anonimo o ancora un matrice di tali oggetti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="eeadf-821">Questi valori non possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="eeadf-821">These values can be nested.</span></span>
  
     <span data-ttu-id="eeadf-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //un tipo anonimo con due campi</span><span class="sxs-lookup"><span data-stu-id="eeadf-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="eeadf-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="eeadf-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="eeadf-824"><a id="SupportedLinqOperators"></a>Elenco di operatori LINQ supportati</span><span class="sxs-lookup"><span data-stu-id="eeadf-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="eeadf-825">Di seguito è riportato un elenco di operatori LINQ supportati nel provider LINQ hello incluso hello DocumentDB .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="eeadf-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="eeadf-826">**Selezionare**: proiezioni traducono toohello SQL SELECT, incluse la costruzione di oggetti</span><span class="sxs-lookup"><span data-stu-id="eeadf-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="eeadf-827">**Dove**: traslazione toohello SQL in cui i filtri e supporta la conversione tra & &, | | e!</span><span class="sxs-lookup"><span data-stu-id="eeadf-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="eeadf-828">operatori SQL toohello</span><span class="sxs-lookup"><span data-stu-id="eeadf-828">toohello SQL operators</span></span>
* <span data-ttu-id="eeadf-829">**SelectMany**: consente la rimozione della clausola JOIN SQL toohello di matrici.</span><span class="sxs-lookup"><span data-stu-id="eeadf-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="eeadf-830">Può essere utilizzato toochain/nidificare le espressioni toofilter sugli elementi di matrice</span><span class="sxs-lookup"><span data-stu-id="eeadf-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="eeadf-831">**OrderBy e OrderByDescending**: converte tooORDER BY crescente/decrescente</span><span class="sxs-lookup"><span data-stu-id="eeadf-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="eeadf-832">Operatori di aggregazione **Count**, **Sum**, **Min**, **Max** e **Average** e relativi equivalenti asincroni **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** e **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="eeadf-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="eeadf-833">**CompareTo**: converte toorange confronti.</span><span class="sxs-lookup"><span data-stu-id="eeadf-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="eeadf-834">In genere usato per le stringhe in quanto non sono confrontabili in .NET</span><span class="sxs-lookup"><span data-stu-id="eeadf-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="eeadf-835">**Richiedere**: converte toohello SQL TOP per limitare i risultati da una query</span><span class="sxs-lookup"><span data-stu-id="eeadf-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="eeadf-836">**Funzioni matematiche**: supporta la conversione da. Abs, Acos, Asin di rete, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, troncare toohello equivalente SQL le funzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="eeadf-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="eeadf-837">**Funzioni stringa**: supporta la conversione da. Concat, Contains, EndsWith del NET, IndexOf, Count, ToLower, TrimStart, Replace, inversa, TrimEnd, StartsWith, SubString, ToUpper toohello equivalente SQL funzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="eeadf-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="eeadf-838">**Funzioni di matrice**: supporta la conversione da. Concat, Contains e conteggio toohello equivalente SQL funzioni predefinite del NET.</span><span class="sxs-lookup"><span data-stu-id="eeadf-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="eeadf-839">**Le funzioni di estensione Geospatial**: supporta la conversione da metodi stub distanza, entro, IsValid e IsValidDetailed toohello equivalente SQL le funzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="eeadf-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="eeadf-840">**Funzione di estensione della funzione definita dall'utente**: conversione supporta da hello stub metodo UserDefinedFunctionProvider.Invoke toohello corrispondente-funzione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eeadf-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="eeadf-841">**Varie**: supporta la conversione di hello coalesce e agli operatori condizionali.</span><span class="sxs-lookup"><span data-stu-id="eeadf-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="eeadf-842">Può essere convertita Contains tooString CONTAINS, ARRAY_CONTAINS o hello IN SQL, a seconda del contesto.</span><span class="sxs-lookup"><span data-stu-id="eeadf-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="eeadf-843">Operatori di query SQL</span><span class="sxs-lookup"><span data-stu-id="eeadf-843">SQL query operators</span></span>
<span data-ttu-id="eeadf-844">Di seguito sono riportati alcuni esempi che illustrano la modalità di conversione alcuni degli operatori di query LINQ standard hello tooCosmos DB le query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="eeadf-845">Operatore Select</span><span class="sxs-lookup"><span data-stu-id="eeadf-845">Select Operator</span></span>
<span data-ttu-id="eeadf-846">sintassi di Hello è `input.Select(x => f(x))`, dove `f` è un'espressione scalare.</span><span class="sxs-lookup"><span data-stu-id="eeadf-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="eeadf-847">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="eeadf-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="eeadf-849">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="eeadf-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="eeadf-851">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="eeadf-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="eeadf-853">Operatore SelectMany</span><span class="sxs-lookup"><span data-stu-id="eeadf-853">SelectMany operator</span></span>
<span data-ttu-id="eeadf-854">sintassi di Hello è `input.SelectMany(x => f(x))`, dove `f` è un'espressione scalare che restituisce un tipo di raccolta.</span><span class="sxs-lookup"><span data-stu-id="eeadf-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="eeadf-855">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="eeadf-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="eeadf-857">Operatore Where</span><span class="sxs-lookup"><span data-stu-id="eeadf-857">Where operator</span></span>
<span data-ttu-id="eeadf-858">sintassi di Hello è `input.Where(x => f(x))`, dove `f` è un'espressione scalare, che restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="eeadf-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="eeadf-859">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="eeadf-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="eeadf-861">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="eeadf-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="eeadf-863">Query SQL composte</span><span class="sxs-lookup"><span data-stu-id="eeadf-863">Composite SQL queries</span></span>
<span data-ttu-id="eeadf-864">Hello sopra gli operatori possono essere composti tooform query più efficace.</span><span class="sxs-lookup"><span data-stu-id="eeadf-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="eeadf-865">Poiché DB Cosmos supporta raccolte annidate, composizione hello può essere concatenato o nidificati.</span><span class="sxs-lookup"><span data-stu-id="eeadf-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="eeadf-866">Concatenazione</span><span class="sxs-lookup"><span data-stu-id="eeadf-866">Concatenation</span></span>
<span data-ttu-id="eeadf-867">sintassi di Hello è `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="eeadf-868">Una query concatenata può iniziare con una query `SelectMany` facoltativa, seguita da più operatori `Select` o `Where`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="eeadf-869">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="eeadf-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="eeadf-871">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="eeadf-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="eeadf-873">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="eeadf-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="eeadf-875">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="eeadf-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="eeadf-877">Annidamento</span><span class="sxs-lookup"><span data-stu-id="eeadf-877">Nesting</span></span>
<span data-ttu-id="eeadf-878">sintassi di Hello è `input.SelectMany(x=>x.Q())` dove Q è un `Select`, `SelectMany`, o `Where` operatore.</span><span class="sxs-lookup"><span data-stu-id="eeadf-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="eeadf-879">In una query annidata, la query interna hello è tooeach applicato elemento della raccolta esterna hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="eeadf-880">Una caratteristica importante è che la query interna hello può fare riferimento a toohello campi di elementi di hello nella raccolta di outer hello come self-join.</span><span class="sxs-lookup"><span data-stu-id="eeadf-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="eeadf-881">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="eeadf-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="eeadf-883">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="eeadf-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="eeadf-885">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="eeadf-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="eeadf-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="eeadf-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="eeadf-887"><a id="ExecutingSqlQueries"></a>Esecuzione di query SQL</span><span class="sxs-lookup"><span data-stu-id="eeadf-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="eeadf-888">Cosmos DB espone risorse tramite un'API REST che può essere chiamata da qualsiasi linguaggio in grado di effettuare richieste HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eeadf-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="eeadf-889">In Cosmos DB sono anche disponibili librerie di programmazione per diversi linguaggi comuni, come NET, Node.js, JavaScript e Python.</span><span class="sxs-lookup"><span data-stu-id="eeadf-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="eeadf-890">Hello API REST e hello diverse librerie tutti supportano l'esecuzione di query tramite SQL.</span><span class="sxs-lookup"><span data-stu-id="eeadf-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="eeadf-891">Hello .NET SDK supporta inoltre query tooSQL LINQ.</span><span class="sxs-lookup"><span data-stu-id="eeadf-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="eeadf-892">Hello seguenti esempi viene illustrato come toocreate una query e li inviano rispetto a un account di database DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eeadf-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="eeadf-893"><a id="RestAPI"></a>API REST</span><span class="sxs-lookup"><span data-stu-id="eeadf-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="eeadf-894">Cosmos DB offre un modello di programmazione aperto RESTful su HTTP.</span><span class="sxs-lookup"><span data-stu-id="eeadf-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="eeadf-895">È possibile effettuare il provisioning degli account di database usando una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeadf-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="eeadf-896">modello di risorsa Cosmos DB Hello è costituito da un set di risorse con un account di database, ognuno dei quali è indirizzabile utilizzando un URI logico e stabile.</span><span class="sxs-lookup"><span data-stu-id="eeadf-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="eeadf-897">Un set di risorse è tooas di cui si fa riferimento un feed in questo documento.</span><span class="sxs-lookup"><span data-stu-id="eeadf-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="eeadf-898">Un account di database è costituito da un set di database, ognuno dei quali include più raccolte, che possono contenere documenti, UDF e altri tipi di risorse.</span><span class="sxs-lookup"><span data-stu-id="eeadf-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="eeadf-899">modello di interazione di base Hello con queste risorse è tramite verbi hello HTTP GET, PUT, POST e DELETE con la relativa interpretazione standard.</span><span class="sxs-lookup"><span data-stu-id="eeadf-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="eeadf-900">verbo POST Hello viene utilizzato per la creazione di una nuova risorsa, per l'esecuzione di una stored procedure o per l'esecuzione di una query DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eeadf-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="eeadf-901">Le query sono sempre operazioni di sola lettura senza nessun effetto collaterale.</span><span class="sxs-lookup"><span data-stu-id="eeadf-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="eeadf-902">Hello esempi seguenti viene illustrato un POST per una query di DocumentDB API effettuata una raccolta che contiene due documenti di esempio hello che abbiamo esaminato finora.</span><span class="sxs-lookup"><span data-stu-id="eeadf-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="eeadf-903">query Hello dispone di un filtro semplice nella proprietà di nome hello JSON.</span><span class="sxs-lookup"><span data-stu-id="eeadf-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="eeadf-904">Si noti utilizzo hello di hello `x-ms-documentdb-isquery` e Content-Type: `application/query+json` toodenote intestazioni che hello operazione è una query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="eeadf-905">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eeadf-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="eeadf-906">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="eeadf-907">Hello secondo esempio viene illustrata una query più complessa che restituisce più risultati da join hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="eeadf-908">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="eeadf-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="eeadf-909">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="eeadf-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="eeadf-910">Se i risultati di una query non possono essere contenuta all'interno di una singola pagina dei risultati, quindi hello API REST restituisce un token di continuazione mediante hello `x-ms-continuation-token` intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="eeadf-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="eeadf-911">I client possono impaginare risultati includendo l'intestazione hello in risultati successivi.</span><span class="sxs-lookup"><span data-stu-id="eeadf-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="eeadf-912">è anche possibile controllare il numero di Hello di risultati per pagina tramite hello `x-ms-max-item-count` intestazione dei numeri.</span><span class="sxs-lookup"><span data-stu-id="eeadf-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="eeadf-913">Se la query specificata hello dispone di una funzione di aggregazione come `COUNT`, quindi pagina query hello può restituire un valore aggregato parzialmente sulla pagina hello dei risultati.</span><span class="sxs-lookup"><span data-stu-id="eeadf-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="eeadf-914">i client Hello deve eseguire un'aggregazione di secondo livello su questi risultati tooproduce hello finale risultati, ad esempio, somma conteggi hello restituiti nel numero totale di hello singole pagine tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="eeadf-915">criteri di verifica coerenza di dati toomanage hello per le query, utilizzare hello `x-ms-consistency-level` intestazione come tutte le richieste API REST.</span><span class="sxs-lookup"><span data-stu-id="eeadf-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="eeadf-916">Per coerenza di sessione, è più recente hello di tooalso obbligatorio eco `x-ms-session-token` intestazione Cookie nella richiesta di query hello.</span><span class="sxs-lookup"><span data-stu-id="eeadf-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="eeadf-917">Hello criteri di indicizzazione della raccolta di query possono inoltre influire sulla coerenza hello dei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="eeadf-918">Con le impostazioni dei criteri di indicizzazione predefiniti di hello, per le raccolte hello indice è sempre aggiornati con il contenuto del documento hello e risultati corrispondano a coerenza hello scelta per i dati di query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="eeadf-919">Se Criteri di indicizzazione hello tooLazy flessibile, le query possono restituire risultati non aggiornati.</span><span class="sxs-lookup"><span data-stu-id="eeadf-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="eeadf-920">Per altre informazioni, vedere [Livelli di coerenza di Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="eeadf-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="eeadf-921">Se hello configurato i criteri di indicizzazione nella raccolta di hello non supportano la query specificata hello, server di database di Azure Cosmos hello restituisce 400 "richiesta non valida".</span><span class="sxs-lookup"><span data-stu-id="eeadf-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="eeadf-922">Questo codice viene restituito per le query di intervallo per ricerche hash (uguaglianza) e per i percorsi esplicitamente esclusi dall'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="eeadf-923">Hello `x-ms-documentdb-query-enable-scan` intestazione può essere specificato tooallow hello query tooperform una scansione quando un indice non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="eeadf-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="eeadf-924">È possibile ottenere le metriche dettagliate sull'esecuzione di query mediante l'impostazione `x-ms-documentdb-populatequerymetrics` intestazione troppo`True`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="eeadf-925">Per altre informazioni, vedere [metriche di query SQL per l'API Azure Cosmos DB DocumentDB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="eeadf-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="eeadf-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="eeadf-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="eeadf-927">Hello .NET SDK supporta LINQ sia SQL l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="eeadf-928">Hello riportato di seguito come query di filtro semplice hello tooperform introdotta in precedenza in questo documento.</span><span class="sxs-lookup"><span data-stu-id="eeadf-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="eeadf-929">In questo esempio vengono confrontate due proprietà per l'uguaglianza all'interno di ciascun documento, usando le proiezioni anonime.</span><span class="sxs-lookup"><span data-stu-id="eeadf-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="eeadf-930">Hello successiva illustra i join, espliciti tramite LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="eeadf-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="eeadf-931">client .NET Hello scorre automaticamente da tutte le pagine hello dei risultati della query in blocchi di foreach hello come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="eeadf-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="eeadf-932">Opzioni introdotte in hello sezione API REST sono disponibili anche in query di Hello hello .NET SDK utilizzando hello `FeedOptions` e `FeedResponse` classi hello CreateDocumentQuery metodo.</span><span class="sxs-lookup"><span data-stu-id="eeadf-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="eeadf-933">numero di Hello di pagine può essere controllata utilizzando hello `MaxItemCount` impostazione.</span><span class="sxs-lookup"><span data-stu-id="eeadf-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="eeadf-934">È possibile controllare in modo esplicito il paging creando `IDocumentQueryable` utilizzando hello `IQueryable` oggetto, quindi leggendo il` ResponseContinuationToken` valori e passarli nuovamente come `RequestContinuationToken` in `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="eeadf-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="eeadf-935">`EnableScanInQuery`può essere set tooenable analisi quando query hello non possono essere supportati da criteri di indicizzazione hello configurato.</span><span class="sxs-lookup"><span data-stu-id="eeadf-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="eeadf-936">Per le raccolte partizionate, è possibile utilizzare `PartitionKey` query di hello toorun su una singola partizione (sebbene DB Cosmos può estrarre automaticamente questo dal testo della query hello), e `EnableCrossPartitionQuery` query toorun che potrebbe essere necessario toobe eseguite in più partizioni.</span><span class="sxs-lookup"><span data-stu-id="eeadf-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="eeadf-937">Fare riferimento troppo[esempi di Azure Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) per altri esempi che includono query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="eeadf-938"><a id="JavaScriptServerSideApi"></a>API lato server JavaScript</span><span class="sxs-lookup"><span data-stu-id="eeadf-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="eeadf-939">COSMOS DB fornisce un modello di programmazione per l'esecuzione di logica dell'applicazione basata su JavaScript direttamente nelle raccolte di hello utilizzando stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="eeadf-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="eeadf-940">logica di JavaScript Hello registrata a livello di raccolta può quindi eseguire operazioni di database su hello operazioni sui documenti hello hello fornito insieme.</span><span class="sxs-lookup"><span data-stu-id="eeadf-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="eeadf-941">Viene quindi eseguito il wrapping di queste operazioni nelle transazioni ACID Ambient.</span><span class="sxs-lookup"><span data-stu-id="eeadf-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="eeadf-942">Hello esempio seguente viene illustrato come una query da toouse hello queryDocuments in toomake hello API server JavaScript all'interno di stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="eeadf-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="eeadf-943"><a id="References"></a>Riferimenti</span><span class="sxs-lookup"><span data-stu-id="eeadf-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="eeadf-944">[Introduzione tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="eeadf-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="eeadf-945">Specifica SQL di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eeadf-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="eeadf-946">Esempi relativi a Azure Cosmos DB .NET</span><span class="sxs-lookup"><span data-stu-id="eeadf-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="eeadf-947">[Livelli di coerenza di Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="eeadf-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="eeadf-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="eeadf-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="eeadf-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="eeadf-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="eeadf-950">Specifiche Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="eeadf-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="eeadf-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="eeadf-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="eeadf-952">Tecniche di valutazione delle query per database di grandi dimensioni [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="eeadf-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="eeadf-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="eeadf-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="eeadf-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="eeadf-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="eeadf-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: un linguaggio non così estraneo per l'elaborazione dati, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="eeadf-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="eeadf-956">G.</span><span class="sxs-lookup"><span data-stu-id="eeadf-956">G.</span></span> <span data-ttu-id="eeadf-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="eeadf-957">Graefe.</span></span> <span data-ttu-id="eeadf-958">framework di catena Hello per l'ottimizzazione delle query.</span><span class="sxs-lookup"><span data-stu-id="eeadf-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="eeadf-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="eeadf-959">IEEE Data Eng.</span></span> <span data-ttu-id="eeadf-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="eeadf-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md