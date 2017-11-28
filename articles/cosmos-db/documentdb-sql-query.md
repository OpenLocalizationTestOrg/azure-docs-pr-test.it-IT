---
title: Query SQL per l'API di DocumentDB di Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="0bd6a-105">Query SQL per l'API di DocumentDB di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0bd6a-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="0bd6a-106">Microsoft Azure Cosmos DB supporta l'esecuzione di query di documenti mediante SQL (Structured Query Language) come linguaggio di query JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="0bd6a-107">Cosmos DB è effettivamente privo di schema.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="0bd6a-108">Grazie all'impegno nei confronti del modello di dati JSON direttamente nel motore del database, fornisce l'indicizzazione automatica dei documenti JSON senza richiedere schemi espliciti o la creazione di indici secondari.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="0bd6a-109">Nella progettazione del linguaggio di query per Cosmos DB sono stati tenuti in considerazione due obiettivi:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="0bd6a-110">Invece di inventare un nuovo linguaggio di query JSON, è stato introdotto il supporto del linguaggio SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="0bd6a-111">SQL è uno dei linguaggi di query più familiari e popolari.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="0bd6a-112">Il linguaggio di query SQL di Cosmos DB fornisce un modello di programmazione formale per le query complesse sui documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="0bd6a-113">Poiché un database di documenti JSON può eseguire JavaScript direttamente nel motore di database, l'obiettivo era di usare il modello di programmazione di JavaScript come base per il linguaggio di query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="0bd6a-114">L'API SQL di DocumentDB trova le sue radici nel sistema di tipi, nella valutazione delle espressioni e nella chiamata di funzioni di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="0bd6a-115">Questo rappresenta a sua volta un modello di programmazione naturale per le proiezioni relazionali, la navigazione gerarchica attraverso i documenti JSON, i self join, query spaziali e la chiamata di funzioni definite dall'utente (UDF) scritte interamente in JavaScript, tra le altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="0bd6a-116">Queste capacità costituiscono la chiave per la riduzione dell'attrito tra l'applicazione e il database e sono di importanza critica per la produttività degli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="0bd6a-117">Si consiglia di iniziare guardando il video seguente, in cui Aravind Ramachandran mostra le funzionalità di query di Cosmos DB, e visitando la pagina [Query Playground](http://www.documentdb.com/sql/demo), in cui è possibile provare Cosmos DB ed eseguire query SQL rispetto a un set di dati predefinito.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="0bd6a-118">Tornare quindi a questo articolo, dove inizia un'esercitazione sulle query SQL in cui verranno illustrati alcuni semplici documenti JSON e comandi SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="0bd6a-119"><a id="GettingStarted"></a>Guida introduttiva ai comandi SQL in Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0bd6a-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="0bd6a-120">Per osservare il funzionamento del linguaggio SQL di Cosmos DB, si inizierà con alcuni semplici documenti JSON e si procederà eseguendo alcune semplici query su tali documenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="0bd6a-121">Considerare questi due documenti JSON come se riguardassero due famiglie.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="0bd6a-122">Con Cosmos DB, non è necessario creare schemi o indici secondari in maniera esplicita.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="0bd6a-123">È sufficiente inserire i documenti JSON in una raccolta di Cosmos DB e successivamente eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="0bd6a-124">In questo caso è illustrato un semplice documento JSON relativo alla famiglia Andersen: i genitori, i figli (e i loro animali domestici), l'indirizzo e le informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="0bd6a-125">Il documento contiene stringhe, numeri, valori booleani, matrici e proprietà annidate.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="0bd6a-126">**Documento**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-126">**Document**</span></span>  

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

<span data-ttu-id="0bd6a-127">Ecco un secondo documento con una sottile differenza: vengono usati `givenName` e `familyName` invece di `firstName` e `lastName`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="0bd6a-128">**Documento**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-128">**Document**</span></span>  

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

<span data-ttu-id="0bd6a-129">A questo punto è possibile provare a eseguire alcune query a fronte di questi dati per comprendere alcuni aspetti chiave dell'API SQL di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="0bd6a-130">Ad esempio, la query seguente restituisce i documenti in cui il campo ID corrisponde a `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="0bd6a-131">Poiché si tratta di un'istruzione `SELECT *`, l'output della query è il documento JSON completo:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="0bd6a-132">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-133">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-133">**Results**</span></span>

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


<span data-ttu-id="0bd6a-134">Si prenda ora in considerazione il caso in cui fosse necessario modificare la formattazione dell'output JSON in una forma differente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="0bd6a-135">Questa query proietta un nuovo oggetto JSON con due campi selezionati, Name e City, quando la città in cui si trova l'indirizzo ha lo stesso nome dello stato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="0bd6a-136">In questo caso, "NY, NY" corrispondono.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="0bd6a-137">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="0bd6a-138">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="0bd6a-139">La query successiva restituisce i nomi di elementi figlio specificati nella famiglia con ID corrispondente a `WakefieldFamily` ordinato in base alla città di residenza.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="0bd6a-140">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="0bd6a-141">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="0bd6a-142">È opportuno prestare attenzione ad alcuni aspetti salienti del linguaggio di query di Cosmos DB attraverso gli esempi finora esaminati:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="0bd6a-143">Poiché l'API SQL di DocumentDB elabora i valori JSON, deve gestire entità con struttura ad albero invece di righe e colonne.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="0bd6a-144">Di conseguenza, il linguaggio consente di fare riferimento ai nodi dell'albero a qualsiasi profondità arbitraria, ad esempio `Node1.Node2.Node3…..Nodem`, in modo analogo al linguaggio SQL relazionale con il riferimento in due parti di `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="0bd6a-145">Il linguaggio strutturato di interrogazione funziona con dati senza schema.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="0bd6a-146">perciò il sistema di tipi deve essere associato in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="0bd6a-147">La stessa espressione potrebbe produrre tipi differenti su documenti differenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="0bd6a-148">Il risultato di una query è un valore JSON valido, ma non è garantito che appartenga a uno schema fisso.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="0bd6a-149">Cosmos DB supporta solo i documenti JSON completi.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="0bd6a-150">Ciò significa che il sistema di tipi e le espressioni sono limitati all'interazione esclusiva con i tipi JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="0bd6a-151">Per altri dettagli, vedere le [specifiche JSON](http://www.json.org/).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="0bd6a-152">Una raccolta di Cosmos DB è un contenitore senza schema dei documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="0bd6a-153">Le relazioni nelle entità di dati all'interno e tra i documenti in una raccolta vengono implicitamente acquisiti dal contenitore e non dalle relazioni chiave primaria e chiave esterna.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="0bd6a-154">È un aspetto importante da sottolineare alla luce dei join tra documenti, descritti più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="0bd6a-155"><a id="Indexing"></a> Indicizzatore di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0bd6a-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="0bd6a-156">Prima di addentrarsi nella sintassi dell'API SQL di DocumentDB, vale la pena esplorare la progettazione dell'indicizzazione di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="0bd6a-157">Lo scopo degli indici di database è gestire le query in varie forme con un consumo di risorse ridotto al minimo (ad esempio CPU, input/output), offrendo al contempo una buona velocità effettiva e basse latenze.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="0bd6a-158">Spesso, la scelta dell'indice corretto per l'interrogazione di un database richiede una lunga pianificazione e sperimentazione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="0bd6a-159">Questo approccio costituisce una sfida per i database senza schema, in cui i dati non si conformano a un rigido schema ed evolvono rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="0bd6a-160">Di conseguenza, durante la progettazione del sottosistema di indicizzazione di Cosmos DB sono stati fissati gli obiettivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="0bd6a-161">Indicizzare i documenti senza schema: il sottosistema di indicizzazione non richiede alcuna informazione sullo schema o supposizioni sullo schema dei documenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="0bd6a-162">Supporto di query relazionali e gerarchiche efficienti e complesse: l'indice supporta il linguaggio di query Cosmos DB in modo efficiente, incluso il supporto per le proiezioni relazionali e gerarchiche.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="0bd6a-163">Supporto per le query coerente sia un volume di scritture sostenuta: per la scrittura ad alta velocità effettiva dei carichi di lavoro con query coerenti, l'indice viene aggiornato in modo incrementale, in modo efficiente e in linea con un volume sostenuto delle operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="0bd6a-164">L'aggiornamento coerente dell'indice è fondamentale per la gestione delle query secondo il livello di coerenza con cui l'utente ha configurato il servizio documenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="0bd6a-165">Supporto per multi-tenancy: dato il modello basato sulla prenotazione per la governance delle risorse tra tenant, gli aggiornamenti dell'indice vengono eseguiti mantenendosi nel budget delle risorse di sistema (CPU, memoria e operazioni di input/output al secondo) allocate per ogni replica.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="0bd6a-166">Per conseguire l'efficienza dei costi, le risorse di archiviazione su disco dell'indice sono vincolate e prevedibili.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="0bd6a-167">Questo è fondamentale perché Cosmos DB consente allo sviluppatore di accettare compromessi basati sul costo tra spese relative all'indice e prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="0bd6a-168">Per informazioni su come configurare i criteri di indicizzazione per una raccolta, vedere gli [esempi relativi a Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) su MSDN.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="0bd6a-169">Verrà ora analizzata più dettagliatamente la sintassi SQL di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="0bd6a-170"><a id="Basics"></a>Elementi di base di una query SQL di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0bd6a-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="0bd6a-171">Ogni query consiste in una clausola SELECT e clausole FROM e WHERE facoltative in base agli standard ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="0bd6a-172">In genere, l'origine nella clausola FROM per ogni query viene enumerata,</span><span class="sxs-lookup"><span data-stu-id="0bd6a-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="0bd6a-173">quindi il filtro nella clausola WHERE viene applicato all'origine per recuperare un sottoinsieme di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="0bd6a-174">Infine, viene usata la clausola SELECT per proiettare i valori JSON richiesti nell'elenco selezionato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="0bd6a-175"><a id="FromClause"></a>Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="0bd6a-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="0bd6a-176">La clausola `FROM <from_specification>` è facoltativa, a meno che l'origine non sia filtrata o proiettata più avanti nella query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="0bd6a-177">Lo scopo di questa query è specificare l'origine dati in base alla quale deve operare la query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="0bd6a-178">Comunemente, l'origine è rappresentata dall'intera raccolta, ma è possibile specificare piuttosto un sottoinsieme della raccolta.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="0bd6a-179">Una query come `SELECT * FROM Families` indica che l'intera raccolta Families è il database di origine in base al quale eseguire l'enumerazione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="0bd6a-180">Invece di usare il nome della raccolta, è possibile usare uno speciale identificatore ROOT per rappresentare la raccolta.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="0bd6a-181">L'elenco seguente include le regole applicate per ogni query:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="0bd6a-182">È possibile effettuare l'aliasing della raccolta, come in `SELECT f.id FROM Families AS f` o semplicemente in `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="0bd6a-183">Qui `f` è l'equivalente di `Families`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="0bd6a-184">`AS` è una parola chiave facoltativa per eseguire l'aliasing dell'identificatore.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="0bd6a-185">Una volta eseguito l'aliasing, non sarà più possibile associare l'origine iniziale.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="0bd6a-186">Ad esempio, la sintassi di `SELECT Families.id FROM Families f` non è valida perché non è più possibile risolvere l'identificatore "Families".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="0bd6a-187">Tutte le proprietà a cui è necessario fare riferimento devono essere complete.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="0bd6a-188">In assenza di una rigorosa aderenza allo schema, ciò viene applicato per evitare eventuali associazioni ambigue.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="0bd6a-189">Di conseguenza, la sintassi di `SELECT id FROM Families f` non è valida perché la proprietà `id` non è associata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="0bd6a-190">Documenti secondari</span><span class="sxs-lookup"><span data-stu-id="0bd6a-190">Subdocuments</span></span>
<span data-ttu-id="0bd6a-191">È anche possibile ridurre il database di origine a un sottoinsieme di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="0bd6a-192">Ad esempio, per enumerare un solo sottoalbero in ogni documento, la sottoradice può quindi diventare l'origine, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="0bd6a-193">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="0bd6a-194">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-194">**Results**</span></span>  

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

<span data-ttu-id="0bd6a-195">Mentre nell'esempio precedente viene usata una matrice come origine, si potrebbe usare anche un oggetto come origine, che è quanto mostrato nell'esempio seguente: qualsiasi valore JSON valido (non indefinito) che può essere trovato nell'origine viene considerato per l'inclusione nel risultato della query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="0bd6a-196">Se alcune famiglie non hanno un valore `address.state` vengono escluse dal risultato della query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="0bd6a-197">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="0bd6a-198">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="0bd6a-199"><a id="WhereClause"></a>Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="0bd6a-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="0bd6a-200">La clausola WHERE (**`WHERE <filter_condition>`**) è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="0bd6a-201">e specifica la condizione (o le condizioni) che i documenti JSON forniti dall'origine devono soddisfare per essere inclusi come parte del risultato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="0bd6a-202">Per essere considerato per il risultato, qualsiasi documento JSON deve valutare le condizioni specificate come "true".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="0bd6a-203">La clausola WHERE viene usata dal livello di indice allo scopo di determinare il sottoinsieme più piccolo in assoluto di documenti di origine che possono fare parte del risultato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="0bd6a-204">La query seguente richiede documenti che contengono una proprietà nome il cui valore è `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="0bd6a-205">Qualsiasi altro documento che non contiene una proprietà nome o il cui valore non corrisponde a `AndersenFamily` verrà escluso.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="0bd6a-206">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-207">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="0bd6a-208">Nell'esempio precedente è stata illustrata una semplice query di uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="0bd6a-209">L'API SQL di DocumentDB supporta anche una varietà di espressioni scalari.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="0bd6a-210">Quelle di uso più comune sono le espressioni binarie e unarie.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="0bd6a-211">Anche i riferimenti di proprietà dell'oggetto JSON sono espressioni valide.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="0bd6a-212">Gli operatori binari seguenti sono attualmente supportati e possono essere usati nelle query come illustrato negli esempi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="0bd6a-213">Aritmetico</span><span class="sxs-lookup"><span data-stu-id="0bd6a-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="0bd6a-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="0bd6a-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0bd6a-215">Bit per bit</span><span class="sxs-lookup"><span data-stu-id="0bd6a-215">Bitwise</span></span></td>    
<td><span data-ttu-id="0bd6a-216">|, &, ^, <<, >>, >>> (spostamento a destra riempimento zero)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0bd6a-217">Logico</span><span class="sxs-lookup"><span data-stu-id="0bd6a-217">Logical</span></span></td>
<td><span data-ttu-id="0bd6a-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="0bd6a-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0bd6a-219">Confronto</span><span class="sxs-lookup"><span data-stu-id="0bd6a-219">Comparison</span></span></td>    
<td><span data-ttu-id="0bd6a-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="0bd6a-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0bd6a-221">String</span><span class="sxs-lookup"><span data-stu-id="0bd6a-221">String</span></span></td>    
<td><span data-ttu-id="0bd6a-222">|| (concatenazione)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="0bd6a-223">Saranno ora prese in esame alcune query che usano gli operatori binari.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="0bd6a-224">Sono supportati anche gli operatori unari +,-, ~ e NOT, che possono essere usati all'interno delle query come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="0bd6a-225">Oltre agli operatori binari e unari, sono consentiti anche i riferimenti di proprietà.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="0bd6a-226">Ad esempio, `SELECT * FROM Families f WHERE f.isRegistered` restituirebbe i documenti JSON contenenti la proprietà `isRegistered` dove il valore della proprietà è uguale al valore JSON `true`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="0bd6a-227">Qualsiasi altro valore (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>` e così via) comporta l'esclusione del documento di origine dai risultati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="0bd6a-228">Operatori di confronto e uguaglianza</span><span class="sxs-lookup"><span data-stu-id="0bd6a-228">Equality and comparison operators</span></span>
<span data-ttu-id="0bd6a-229">La tabella seguente illustra il risultato dei confronti di uguaglianza nell'API SQL di DocumentDB tra due tipi JSON qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="0bd6a-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="0bd6a-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="0bd6a-233">
            <strong>Boolean</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="0bd6a-234">
            <strong>Number</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="0bd6a-235">
            <strong>String</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="0bd6a-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="0bd6a-237">
            <strong>Array</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="0bd6a-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-254">
            <strong>Boolean<strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="0bd6a-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-262">
            <strong>Number<strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="0bd6a-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-270">
            <strong>String<strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="0bd6a-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="0bd6a-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="0bd6a-286">
            <strong>Array<strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="0bd6a-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="0bd6a-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="0bd6a-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="0bd6a-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="0bd6a-294">Per gli altri operatori di confronto, ad esempio >, >=, !=, < e <=, si applicano le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="0bd6a-295">Confronto tra risultati dei tipi in Undefined.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="0bd6a-296">Confronto tra i risultati di due oggetti o due matrici in Undefined.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="0bd6a-297">Se il risultato dell'espressione scalare nel filtro è Undefined, il documento corrispondente non verrebbe incluso nel risultato, perché Undefined non è logicamente uguale a "true".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="0bd6a-298">Parola chiave BETWEEN</span><span class="sxs-lookup"><span data-stu-id="0bd6a-298">BETWEEN keyword</span></span>
<span data-ttu-id="0bd6a-299">È possibile usare anche la parola chiave BETWEEN per esprimere query su intervalli di valori come in SQL ANSI.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="0bd6a-300">La parola BETWEEN può essere utilizzata con stringhe o numeri.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="0bd6a-301">Ad esempio, questa query restituisce tutti i documenti della famiglia in cui la classe frequentata dal primo figlio sia compresa tra 1 e 5 (inclusi).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="0bd6a-302">A differenza di SQL ANSI, è possibile usare la clausola BETWEEN anche nella clausola FROM, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="0bd6a-303">Per accelerare l'esecuzione della query, creare un criterio di indicizzazione che usa un tipo di indice di intervallo su qualsiasi proprietà/percorso numerico filtrato nella clausola BETWEEN.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="0bd6a-304">La differenza principale tra l'uso di BETWEEN nell'API di DocumentDB e ANSI SQL consiste nel fatto che è possibile esprimere le query di intervallo su proprietà di tipo misto. Ad esempio, "grade" può essere un numero (5) in alcuni documenti e stringhe in altri ("grade4").</span><span class="sxs-lookup"><span data-stu-id="0bd6a-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="0bd6a-305">In questi casi, come in JavaScript, un confronto tra due tipi diversi restituisce un risultato "undefined" e il documento viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="0bd6a-306">Operatori logici (AND, OR e NOT)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="0bd6a-307">Gli operatori logici funzionano con valori booleani.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="0bd6a-308">Le tabelle di veridicità logica per questi operatori sono illustrate di seguito.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="0bd6a-309">OPPURE</span><span class="sxs-lookup"><span data-stu-id="0bd6a-309">OR</span></span> | <span data-ttu-id="0bd6a-310">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-310">True</span></span> | <span data-ttu-id="0bd6a-311">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-311">False</span></span> | <span data-ttu-id="0bd6a-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0bd6a-313">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-313">True</span></span> |<span data-ttu-id="0bd6a-314">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-314">True</span></span> |<span data-ttu-id="0bd6a-315">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-315">True</span></span> |<span data-ttu-id="0bd6a-316">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-316">True</span></span> |
| <span data-ttu-id="0bd6a-317">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-317">False</span></span> |<span data-ttu-id="0bd6a-318">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-318">True</span></span> |<span data-ttu-id="0bd6a-319">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-319">False</span></span> |<span data-ttu-id="0bd6a-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-320">Undefined</span></span> |
| <span data-ttu-id="0bd6a-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-321">Undefined</span></span> |<span data-ttu-id="0bd6a-322">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-322">True</span></span> |<span data-ttu-id="0bd6a-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-323">Undefined</span></span> |<span data-ttu-id="0bd6a-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-324">Undefined</span></span> |

| <span data-ttu-id="0bd6a-325">AND</span><span class="sxs-lookup"><span data-stu-id="0bd6a-325">AND</span></span> | <span data-ttu-id="0bd6a-326">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-326">True</span></span> | <span data-ttu-id="0bd6a-327">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-327">False</span></span> | <span data-ttu-id="0bd6a-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0bd6a-329">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-329">True</span></span> |<span data-ttu-id="0bd6a-330">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-330">True</span></span> |<span data-ttu-id="0bd6a-331">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-331">False</span></span> |<span data-ttu-id="0bd6a-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-332">Undefined</span></span> |
| <span data-ttu-id="0bd6a-333">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-333">False</span></span> |<span data-ttu-id="0bd6a-334">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-334">False</span></span> |<span data-ttu-id="0bd6a-335">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-335">False</span></span> |<span data-ttu-id="0bd6a-336">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-336">False</span></span> |
| <span data-ttu-id="0bd6a-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-337">Undefined</span></span> |<span data-ttu-id="0bd6a-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-338">Undefined</span></span> |<span data-ttu-id="0bd6a-339">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-339">False</span></span> |<span data-ttu-id="0bd6a-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-340">Undefined</span></span> |

| <span data-ttu-id="0bd6a-341">NOT</span><span class="sxs-lookup"><span data-stu-id="0bd6a-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="0bd6a-342">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-342">True</span></span> |<span data-ttu-id="0bd6a-343">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-343">False</span></span> |
| <span data-ttu-id="0bd6a-344">False</span><span class="sxs-lookup"><span data-stu-id="0bd6a-344">False</span></span> |<span data-ttu-id="0bd6a-345">True</span><span class="sxs-lookup"><span data-stu-id="0bd6a-345">True</span></span> |
| <span data-ttu-id="0bd6a-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-346">Undefined</span></span> |<span data-ttu-id="0bd6a-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="0bd6a-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="0bd6a-348">Parola chiave IN</span><span class="sxs-lookup"><span data-stu-id="0bd6a-348">IN keyword</span></span>
<span data-ttu-id="0bd6a-349">La parola chiave IN consente di controllare se un valore specificato corrisponde a qualsiasi valore in un elenco.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="0bd6a-350">Ad esempio, questa query restituisce tutti i documenti famiglia dove l'id è uno dei "WakefieldFamily" o "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="0bd6a-351">In questo esempio restituisce tutti i documenti in cui lo stato è uno dei valori specificati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="0bd6a-352">Operatori Ternary (?) e Coalesce (??)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="0bd6a-353">Gli operatori Ternary e Coalesce possono essere usati per compilare espressioni condizionali, analogamente ai linguaggi di programmazione più diffusi come C# e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="0bd6a-354">L'operatore Ternary (?) può essere molto comodo quando si costruiscono rapidamente nuove proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="0bd6a-355">Ad esempio, ora è possibile scrivere query per classificare i livelli di istruzione in forma leggibile, ad esempio principiante/intermedio/avanzati, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="0bd6a-356">È anche possibile annidare le chiamate all'operatore come nella query seguente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="0bd6a-357">Come con altri operatori di query, se le proprietà cui viene fatto riferimento nell'espressione condizionale non sono presenti in alcun documento o se i tipi confrontati sono diversi, tali documenti vengono esclusi dai risultati della query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="0bd6a-358">L'operatore Coalesce (??) può essere usato per verificare se una proprietà è presente</span><span class="sxs-lookup"><span data-stu-id="0bd6a-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="0bd6a-359">(definita) in un documento.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-359">is defined) in a document.</span></span> <span data-ttu-id="0bd6a-360">Questo risulta utile per le query su dati semistrutturati o di tipo misto</span><span class="sxs-lookup"><span data-stu-id="0bd6a-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="0bd6a-361">Ad esempio, questa query restituisce il valore "lastName" se è presente oppure il valore "surname" se non è presente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="0bd6a-362"><a id="EscapingReservedKeywords"></a>Funzione di accesso della proprietà di delimitazione</span><span class="sxs-lookup"><span data-stu-id="0bd6a-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="0bd6a-363">È anche possibile accedere alle proprietà mediante l'operatore della proprietà di delimitazione `[]`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="0bd6a-364">Ad esempio, la sintassi di `SELECT c.grade` and `SELECT c["grade"]` sono equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="0bd6a-365">Questa sintassi risulta utile quando occorre usare i caratteri di escape per una proprietà che contiene spazi, caratteri speciali o condivide lo stesso nome di una parola chiave SQL o una parola riservata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="0bd6a-366"><a id="SelectClause"></a>Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="0bd6a-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="0bd6a-367">La clausola SELECT (**`SELECT <select_list>`**) è obbligatoria e specifica quali valori vengono recuperati dalla query, proprio come in ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="0bd6a-368">Il sottoinsieme filtrato dai documenti di origine viene passato alla fase di proiezione, in cui vengono recuperati i valori JSON specificati viene costruito un nuovo oggetto JSON, per ogni input passato ad esso.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="0bd6a-369">L'esempio seguente illustra una tipica query SELECT.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="0bd6a-370">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-371">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="0bd6a-372">Proprietà annidate</span><span class="sxs-lookup"><span data-stu-id="0bd6a-372">Nested properties</span></span>
<span data-ttu-id="0bd6a-373">Nell'esempio seguente vengono proiettate due proprietà annidate `f.address.state` and `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="0bd6a-374">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-375">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="0bd6a-376">La proiezione supporta anche le espressioni JSON, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="0bd6a-377">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-378">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="0bd6a-379">Verrà ora esaminato il ruolo di `$1` .</span><span class="sxs-lookup"><span data-stu-id="0bd6a-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="0bd6a-380">La clausola `SELECT` deve creare un oggetto JSON e, poiché non è stata fornita alcuna chiave, verranno usati i nomi di variabile di argomento implicita che iniziano per `$1`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="0bd6a-381">Ad esempio, questa query restituisce due variabili di argomento implicite, etichettate `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="0bd6a-382">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-383">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="0bd6a-384">Aliasing</span><span class="sxs-lookup"><span data-stu-id="0bd6a-384">Aliasing</span></span>
<span data-ttu-id="0bd6a-385">L'esempio precedente verrà ora esteso con l'aliasing esplicito dei valori.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="0bd6a-386">AS è la parola chiave usata per l'aliasing.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="0bd6a-387">È facoltativo, come è possibile vedere durante la proiezione del secondo valore come `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="0bd6a-388">Nel caso in cui una query avesse due proprietà con lo stesso nome, è necessario usare l'aliasing per rinominare una o entrambe le proprietà, in modo da evitare ambiguità nel risultato proiettato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="0bd6a-389">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-390">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="0bd6a-391">Espressioni scalari</span><span class="sxs-lookup"><span data-stu-id="0bd6a-391">Scalar expressions</span></span>
<span data-ttu-id="0bd6a-392">Oltre ai riferimenti di proprietà, la clausola SELECT supporta anche le espressioni scalari, ad esempio le costanti, le espressioni aritmetiche, le espressioni logiche e così via. Ad esempio, ecco una semplice query "Hello World".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="0bd6a-393">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="0bd6a-394">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="0bd6a-395">Di seguito è presentato un esempio più complesso che usa un'espressione scalare.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="0bd6a-396">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="0bd6a-397">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="0bd6a-398">Nell'esempio seguente, il risultato dell'espressione scalare è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="0bd6a-399">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="0bd6a-400">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="0bd6a-401">Creazione di oggetti e matrici</span><span class="sxs-lookup"><span data-stu-id="0bd6a-401">Object and array creation</span></span>
<span data-ttu-id="0bd6a-402">Un'altra funzione fondamentale dell'API SQL di DocumentDB è la creazione di matrici/oggetti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="0bd6a-403">Nell'esempio precedente si è osservato che è stato creato un nuovo oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="0bd6a-404">In modo analogo, è possibile creare matrici, come illustrato negli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="0bd6a-405">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="0bd6a-406">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-406">**Results**</span></span>  

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

### <span data-ttu-id="0bd6a-407"><a id="ValueKeyword"></a>Parola chiave VALUE</span><span class="sxs-lookup"><span data-stu-id="0bd6a-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="0bd6a-408">La parola chiave **VALUE** consente di restituire un valore JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="0bd6a-409">Ad esempio, la query mostrata di seguito restituisce l'espressione scalare `"Hello World"` invece di `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="0bd6a-410">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="0bd6a-411">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="0bd6a-412">La query seguente restituisce il valore JSON senza l'etichetta `"address"` nei risultati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="0bd6a-413">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="0bd6a-414">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-414">**Results**</span></span>  

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

<span data-ttu-id="0bd6a-415">L'esempio seguente estende questo risultato mostrando come restituire valori primitivi JSON (il livello foglia dell'albero JSON).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="0bd6a-416">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="0bd6a-417">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="0bd6a-418">Operatore *</span><span class="sxs-lookup"><span data-stu-id="0bd6a-418">* Operator</span></span>
<span data-ttu-id="0bd6a-419">L'operatore speciale (*) è supportato per proiettare il documento così com'è.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="0bd6a-420">Quando usato, deve essere l'unico campo proiettato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="0bd6a-421">Benché una query come `SELECT * FROM Families f` sia valida, `SELECT VALUE * FROM Families f ` e `SELECT *, f.id FROM Families f ` non lo sono.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="0bd6a-422">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="0bd6a-423">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-423">**Results**</span></span>

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

### <span data-ttu-id="0bd6a-424"><a id="TopKeyword"></a>Operatore TOP</span><span class="sxs-lookup"><span data-stu-id="0bd6a-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="0bd6a-425">La parola chiave TOP può essere usata per limitare il numero di valori restituiti da una query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="0bd6a-426">Se si usa TOP in combinazione con la clausola ORDER BY, il set di risultati è limitato al primo numero N di valori ordinati. In caso contrario, restituisce il primo numero N di risultati in un ordine non definito.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="0bd6a-427">Come procedura consigliata, in un'istruzione SELECT, usare sempre una clausola ORDER BY con la clausola TOP.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="0bd6a-428">Questo è l'unico modo per indicare in modo prevedibile le righe interessate dalla clausola TOP.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="0bd6a-429">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="0bd6a-430">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-430">**Results**</span></span>

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

<span data-ttu-id="0bd6a-431">È possibile usare TOP con un valore costante (come illustrato in precedenza) o con un valore della variabile usando le query con parametri.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="0bd6a-432">Per altre informazioni dettagliate, vedere le query con parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="0bd6a-433"><a id="Aggregates"></a>Funzioni di aggregazione</span><span class="sxs-lookup"><span data-stu-id="0bd6a-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="0bd6a-434">È anche possibile eseguire le aggregazioni nella clausola `SELECT`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="0bd6a-435">Le funzioni di aggregazione eseguono un calcolo su un set di valori e restituiscono un singolo valore.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="0bd6a-436">Ad esempio, la query seguente restituisce il numero di documenti della famiglia all'interno della raccolta.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="0bd6a-437">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="0bd6a-438">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="0bd6a-439">È anche possibile restituire il valore scalare della funzione di aggregazione tramite la parola chiave `VALUE`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="0bd6a-440">Ad esempio, la query seguente restituisce il numero di valori come un singolo numero:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="0bd6a-441">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="0bd6a-442">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="0bd6a-443">È anche possibile eseguire aggregazioni combinate a filtri.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="0bd6a-444">Ad esempio, la query seguente restituisce il numero di documenti con un indirizzo nello Stato di Washington.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="0bd6a-445">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="0bd6a-446">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="0bd6a-447">La tabella seguente mostra l'elenco delle funzioni di aggregazione supportate nell'API di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="0bd6a-448">`SUM`e `AVG` vengono eseguite su valori numerici, mentre `COUNT`, `MIN` e `MAX` possono essere eseguite su numeri, stringhe, valori booleani e valori null.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="0bd6a-449">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="0bd6a-449">Usage</span></span> | <span data-ttu-id="0bd6a-450">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0bd6a-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="0bd6a-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="0bd6a-451">COUNT</span></span> | <span data-ttu-id="0bd6a-452">Restituisce il numero di elementi nell'espressione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="0bd6a-453">SUM</span><span class="sxs-lookup"><span data-stu-id="0bd6a-453">SUM</span></span>   | <span data-ttu-id="0bd6a-454">Restituisce la somma dei valori nell'espressione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="0bd6a-455">MIN</span><span class="sxs-lookup"><span data-stu-id="0bd6a-455">MIN</span></span>   | <span data-ttu-id="0bd6a-456">Restituisce il valore minimo nell'espressione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="0bd6a-457">MAX</span><span class="sxs-lookup"><span data-stu-id="0bd6a-457">MAX</span></span>   | <span data-ttu-id="0bd6a-458">Restituisce il valore massimo nell'espressione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="0bd6a-459">MEDIA</span><span class="sxs-lookup"><span data-stu-id="0bd6a-459">AVG</span></span>   | <span data-ttu-id="0bd6a-460">Restituisce la media dei valori nell'espressione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="0bd6a-461">Le aggregazioni possono essere eseguite anche sui risultati di un'iterazione della matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="0bd6a-462">Per altre informazioni, vedere [Array Iteration in Queries](#Iteration) (Iterazione della matrice nelle query).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="0bd6a-463">Tenere presente che quando si usa Esplora Query del portale di Azure, le query di aggregazione possono restituire risultati parzialmente aggregati su una pagina di query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="0bd6a-464">L'SDK genera un singolo valore cumulativo in tutte le pagine.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="0bd6a-465">Per eseguire query di aggregazione tramite codice, è necessario .NET SDK 1.12.0, .NET Core SDK 1.1.0 o SDK per Java 1.9.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="0bd6a-466"><a id="OrderByClause"></a>Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="0bd6a-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="0bd6a-467">Come in SQL ANSI, è possibile includere una clausola Order By facoltativa durante l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="0bd6a-468">La clausola può includere un argomento ASC/DESC facoltativo per specificare l'ordine in cui i risultati devono essere recuperati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="0bd6a-469">Ad esempio, la query seguente recupera le famiglie in ordine di nome della città di residenza.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="0bd6a-470">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="0bd6a-471">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-471">**Results**</span></span>

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

<span data-ttu-id="0bd6a-472">La query seguente recupera le famiglie in ordine di data di creazione, archiviata come numero che rappresenta il periodo, ovvero il tempo trascorso dall'1 gennaio 1970 in secondi.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="0bd6a-473">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="0bd6a-474">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-474">**Results**</span></span>

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

## <span data-ttu-id="0bd6a-475"><a id="Advanced"></a>Concetti avanzati relativi ai database e alle query SQL</span><span class="sxs-lookup"><span data-stu-id="0bd6a-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="0bd6a-476"><a id="Iteration"></a>Iterazione</span><span class="sxs-lookup"><span data-stu-id="0bd6a-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="0bd6a-477">Nell'API SQL di DocumentDB è stato aggiunto un nuovo costrutto tramite la parola chiave **IN** per fornire supporto all'iterazione nelle matrici JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="0bd6a-478">L'origine FROM fornisce supporto per l'iterazione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="0bd6a-479">Esaminare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-479">Let's start with the following example:</span></span>

<span data-ttu-id="0bd6a-480">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="0bd6a-481">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-481">**Results**</span></span>  

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

<span data-ttu-id="0bd6a-482">Esaminare ora un'altra query che esegue l'iterazione sui figli nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="0bd6a-483">Notare la differenza nella matrice di output.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-483">Note the difference in the output array.</span></span> <span data-ttu-id="0bd6a-484">Questo esempio suddivide `children` e converte i risultati in un'unica matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="0bd6a-485">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="0bd6a-486">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-486">**Results**</span></span>  

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

<span data-ttu-id="0bd6a-487">Può essere usato per filtrare ulteriormente ciascuna voce individuale della matrice, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="0bd6a-488">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="0bd6a-489">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="0bd6a-490">È anche possibile eseguire l'aggregazione sul risultato dell'iterazione della matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="0bd6a-491">Ad esempio, la query seguente conta il numero di figli in tutte le famiglie.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="0bd6a-492">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="0bd6a-493">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="0bd6a-494"><a id="Joins"></a>Join</span><span class="sxs-lookup"><span data-stu-id="0bd6a-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="0bd6a-495">In un database relazionale, la necessità creare un join tra tabelle è importante.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="0bd6a-496">È il corollario logico della progettazione di schemi normalizzati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="0bd6a-497">Al contrario, l'API di DocumentDB gestisce un modello dati denormalizzato di documenti senza schema.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="0bd6a-498">È l'equivalente logico di un "self-join".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="0bd6a-499">La sintassi supportata dal linguaggio è <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="0bd6a-500">In generale, restituisce un set di tuple **N** (tupla con valori **N**).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="0bd6a-501">Ogni tupla ha valori prodotti dall'iterazione di tutti gli alias della raccolta sui rispettivi set.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="0bd6a-502">In altri termini, si tratta del prodotto incrociato completo dei set che partecipano al join.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="0bd6a-503">Gli esempi seguenti illustrano il funzionamento della clausola JOIN.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="0bd6a-504">Nell'esempio seguente, il risultato è vuoto perché il prodotto incrociato di ciascun documento dall'origine e un set vuoto è a sua volta vuoto.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="0bd6a-505">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="0bd6a-506">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="0bd6a-507">Nell'esempio seguente il join avviene tra la radice del documento e la sottoradice di `children`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="0bd6a-508">È un prodotto incrociato tra due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="0bd6a-509">Il fatto che i figli siano una matrice non è effettivo nel JOIN in quanto in questo esempio si ha a che fare con una singola radice che è anche la matrice dei figli.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="0bd6a-510">Di conseguenza, il risultato contiene solo due risultati, perché il prodotto incrociato di ogni documento con la matrice produce esattamente un solo documento.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="0bd6a-511">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="0bd6a-512">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="0bd6a-513">L'esempio seguente illustra un join più convenzionale:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="0bd6a-514">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="0bd6a-515">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-515">**Results**</span></span>

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



<span data-ttu-id="0bd6a-516">Per prima cosa occorre notare che il valore `from_source` della clausola **JOIN** è un iteratore.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="0bd6a-517">Pertanto il flusso in questo caso è il seguente:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="0bd6a-518">Espandere ciascun elemento figlio **c** nella matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="0bd6a-519">Applicare un prodotto incrociato con la radice del documento **f** con ogni elemento figlio **c** che è stato convertito nel primo passaggio.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="0bd6a-520">Infine, proiettare solo la proprietà nome **f** dell'oggetto radice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="0bd6a-521">Il primo documento (`AndersenFamily`) contiene solo un elemento figlio, quindi il set di risultati contiene un singolo oggetto corrispondente a questo documento.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="0bd6a-522">Il secondo documento (`WakefieldFamily`) contiene due elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="0bd6a-523">Quindi, il prodotto incrociato genera un oggetto separato per ogni figli, dando come risultato due oggetti, uno per ogni figlio corrispondente a questo documento.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="0bd6a-524">I campi radice in entrambi i documenti sono uguali, proprio come ci si aspetterebbe in un prodotto incrociato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="0bd6a-525">La vera utilità del JOIN consiste nel formare tuple dal prodotto incrociato in una forma che altrimenti sarebbe difficile proiettare.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="0bd6a-526">Come illustrato nell'esempio seguente, è possibile filtrare la combinazione di una tupla che consenta all'utente di scegliere una condizione soddisfatta dall'insieme delle tuple.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="0bd6a-527">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="0bd6a-528">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-528">**Results**</span></span>

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



<span data-ttu-id="0bd6a-529">Questo esempio è un'estensione naturale del precedente e illustra l'esecuzione di un doppio join.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="0bd6a-530">Il prodotto incrociato può quindi essere visualizzato come lo pseudo-codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

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

<span data-ttu-id="0bd6a-531">`AndersenFamily` ha un figlio che ha un animale domestico.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="0bd6a-532">Il prodotto incrociato genera dunque una riga (1\*1\*1) da questa famiglia.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="0bd6a-533">Tuttavia, la famiglia WakefieldFamily ha due figli, ma un solo figlio, "Jesse", ha animali domestici.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="0bd6a-534">Jesse ha però due animali domestici.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-534">Jesse has two pets though.</span></span> <span data-ttu-id="0bd6a-535">il prodotto incrociato genera dunque 1\*1\*2 = 2 righe da questa famiglia.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="0bd6a-536">Nell'esempio successivo è presente un filtro aggiuntivo su `pet`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="0bd6a-537">In tal modo vengono escluse tutte le tuple laddove il nome dell'animale non è "Shadow".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="0bd6a-538">Notare che è possibile creare tuple da matrici, filtrare in base a uno qualsiasi degli elementi della tupla e proiettare qualsiasi combinazione degli elementi.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="0bd6a-539">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="0bd6a-540">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="0bd6a-541"><a id="JavaScriptIntegration"></a>Integrazione JavaScript</span><span class="sxs-lookup"><span data-stu-id="0bd6a-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="0bd6a-542">Azure Cosmos DB offre un modello di programmazione per l'esecuzione di logica dell'applicazione basata su JavaScript direttamente nelle raccolte in termini di stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="0bd6a-543">Ciò consente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-543">This allows for both:</span></span>

* <span data-ttu-id="0bd6a-544">Possibilità di eseguire query e operazioni CRUD transazionali con prestazioni elevate a fronte dei documenti in una raccolta grazie alla stretta integrazione del runtime JavaScript direttamente nel motore di database.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="0bd6a-545">Modellazione naturale del flusso di controllo, definizione dell'ambito delle variabili e assegnazione e integrazione di primitivi di gestione delle eccezioni con transazioni di database.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="0bd6a-546">Per altri dettagli sul supporto di Azure Cosmos DB per l'integrazione di JavaScript, vedere la documentazione relativa alla programmabilità lato server di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="0bd6a-547"><a id="UserDefinedFunctions"></a>Funzioni definite dall'utente (UDF)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="0bd6a-548">Oltre ai tipi già specificati in questo articolo, l'API SQL di DocumentDB offre il supporto per le funzioni definite dall'utente (UDF).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="0bd6a-549">In particolare, le UDF scalari sono supportate laddove gli sviluppatori possono passare zero o molti argomenti e restituire un unico argomento.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="0bd6a-550">Verrà quindi eseguito un controllo per verificare che ciascuno di questi argomenti sia un valore JSON legale.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="0bd6a-551">La sintassi dell'API SQL di DocumentDB viene estesa per supportare la logica delle applicazioni personalizzata usando le funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="0bd6a-552">Le UDF possono essere registrate con l'API di DocumentDB ed è quindi possibile fare loro riferimento come parte di una query SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="0bd6a-553">In effetti, le UDF sono progettate espressamente per essere richiamate dalle query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="0bd6a-554">Come corollario a questa scelta, le UDF non hanno accesso all'oggetto di contesto a cui possono invece accedere altri tipi di Javascript (stored procedure e trigger).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="0bd6a-555">Poiché le query vengono eseguite in sola lettura, è possibile eseguirle sulle repliche primarie o secondarie.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="0bd6a-556">Di conseguenza, a differenza di altri tipi di JavaScript, le UDF vengono progettate per l'esecuzione sulle repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="0bd6a-557">Di seguito è riportato un esempio di come è possibile registrare una UDF nel database di Cosmos DB, in maniera specifica in una raccolta di documenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="0bd6a-558">Nell'esempio precedente è stata creata una UDF, denominata `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="0bd6a-559">Accetta due valori stringa JSON `input` and `pattern` e controlla se il primo corrisponde al modello specificato nel secondo mediante la funzione string.match() di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="0bd6a-560">È ora possibile usare questa UDF in una query in una proiezione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="0bd6a-561">Le UDF devono essere qualificate con il prefisso con distinzione tra maiuscole e minuscole "udf."</span><span class="sxs-lookup"><span data-stu-id="0bd6a-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="0bd6a-562">quando chiamate dall'interno delle query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="0bd6a-563">Prima del 17/03/2015, Cosmos DB supportava le chiamate UDF senza il prefisso "udf.",</span><span class="sxs-lookup"><span data-stu-id="0bd6a-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="0bd6a-564">come SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="0bd6a-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="0bd6a-565">Questo modello di chiamata è stato deprecato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="0bd6a-566">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="0bd6a-567">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="0bd6a-568">È anche possibile usare l'UDF all'interno di un filtro, come mostrato nell'esempio seguente, anch'esso qualificato con il</span><span class="sxs-lookup"><span data-stu-id="0bd6a-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="0bd6a-569">prefisso:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-569">prefix:</span></span>

<span data-ttu-id="0bd6a-570">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="0bd6a-571">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="0bd6a-572">In sostanza, le UDF sono espressioni scalari valide che è possibile usare sia nelle proiezioni sia nei filtri.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="0bd6a-573">Per ampliare la potenza delle UDF, verrà ora analizzato un altro esempio che prevede la logica condizionale:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="0bd6a-574">Di seguito è riportato un esempio per l'esercitazione con le UDF.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="0bd6a-575">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="0bd6a-576">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-576">**Results**</span></span>

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


<span data-ttu-id="0bd6a-577">Come mostrato dagli esempi precedenti, le UDF integrano la potenza del linguaggio JavaScript con quella dell'API SQL di DocumentDB per fornire un'interfaccia programmabile avanzata con la quale eseguire una logica condizionale e procedurale complessa con l'ausilio delle capacità di runtime JavaScript integrate.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="0bd6a-578">L'API SQL di DocumentDB fornisce gli argomenti alle UDF per ogni documento nel database di origine nella fase corrente (clausola WHERE o clausola SELECT) di elaborazione della UDF.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="0bd6a-579">Il risultato verrà incorporato in maniera uniforme nella pipeline di esecuzione generale.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="0bd6a-580">Se le proprietà a cui fanno riferimento i parametri della UDF non sono disponibili nel valore JSON, il parametro verrà considerato come Undefined, quindi la chiamata alla UDF verrà interamente ignorata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="0bd6a-581">Analogamente, se il risultato della UDF è Undefined, non verrà incluso nel risultato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="0bd6a-582">Riepilogando, le UDF sono un ottimo strumento per eseguire una logica di business complessa come parte della query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="0bd6a-583">Valutazione degli operatori</span><span class="sxs-lookup"><span data-stu-id="0bd6a-583">Operator evaluation</span></span>
<span data-ttu-id="0bd6a-584">Essendo un database JSON, Cosmos DB esegue un confronto con gli operatori JavaScript e la relativa semantica di valutazione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="0bd6a-585">Benché Cosmos DB provi a mantenere la semantica di JavaScript in termini di supporto JSON, la valutazione dell'operazione devia in alcune istanze.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="0bd6a-586">A differenza del tradizionale linguaggio SQL, nell'API SQL di DocumentDB spesso i tipi di valori non sono noti fino al loro recupero dal database.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="0bd6a-587">Per poter eseguire le query in maniera efficiente, gran parte degli operatori ha rigorosi requisiti di tipi.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="0bd6a-588">L'API SQL di DocumentDB non esegue conversioni implicite, a differenza di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="0bd6a-589">Ad esempio, una query come `SELECT * FROM Person p WHERE p.Age = 21` corrisponde a documenti che contengono una proprietà Age il cui valore è 21.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="0bd6a-590">Qualsiasi altro documento la cui proprietà Age corrisponde alla stringa "21", o ad altre possibili variazioni come "021", "21.0", "0021", "00021" e così via, non verrà trovato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="0bd6a-591">Questo comportamento è diverso da quanto avviene in JavaScript, che consente di eseguire implicitamente il cast dei valori di stringa al numero (in base all'operatore, ad esempio: ==).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="0bd6a-592">Questa scelta è fondamentale per la ricerca di indici corrispondenti nell'API SQL di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="0bd6a-593">Query SQL con parametri</span><span class="sxs-lookup"><span data-stu-id="0bd6a-593">Parameterized SQL queries</span></span>
<span data-ttu-id="0bd6a-594">Cosmos DB supporta le query con parametri espressi con la consueta notazione @.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="0bd6a-595">SQL con parametri fornisce solide capacità di gestione ed escape dell'input utente, evitando l'esposizione accidentale di dati mediante attacchi SQL injection.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="0bd6a-596">Ad esempio, è possibile scrivere una query che accetta come parametri il cognome e lo stato di residenza e quindi eseguirla per diversi valori di cognome e stato di residenza in base all'input dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="0bd6a-597">Questa richiesta può quindi essere inviata a Cosmos DB come query con parametri JSON, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="0bd6a-598">L'argomento può essere impostato su TOP mediante query con parametri, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="0bd6a-599">I valori dei parametri possono essere qualsiasi valore JSON valido (stringhe, numeri, valori booleani, valori null, persino matrici o valori JSON annidati).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="0bd6a-600">Inoltre, dato che Cosmos DB è senza schema, i parametri non vengono convalidati rispetto a qualsiasi tipo.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="0bd6a-601"><a id="BuiltinFunctions"></a>Funzioni predefinite</span><span class="sxs-lookup"><span data-stu-id="0bd6a-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="0bd6a-602">Cosmos DB supporta anche una serie di funzioni predefinite per le operazioni comuni, che possono essere usate all'interno di query come le funzioni definite dall'utente (UDF).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="0bd6a-603">Gruppo di funzioni</span><span class="sxs-lookup"><span data-stu-id="0bd6a-603">Function group</span></span>          | <span data-ttu-id="0bd6a-604">Operazioni</span><span class="sxs-lookup"><span data-stu-id="0bd6a-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0bd6a-605">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="0bd6a-605">Mathematical functions</span></span>  | <span data-ttu-id="0bd6a-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, gradi, PI, radianti, SIN e TAN</span><span class="sxs-lookup"><span data-stu-id="0bd6a-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="0bd6a-607">Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="0bd6a-607">Type checking functions</span></span> | <span data-ttu-id="0bd6a-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="0bd6a-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="0bd6a-609">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="0bd6a-609">String functions</span></span>        | <span data-ttu-id="0bd6a-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, sinistra, lunghezza, inferiore, LTRIM, REPLACE, replica, inversa, destra, RTRIM, STARTSWITH, SUBSTRING e superiore</span><span class="sxs-lookup"><span data-stu-id="0bd6a-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="0bd6a-611">Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="0bd6a-611">Array functions</span></span>         | <span data-ttu-id="0bd6a-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH e ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="0bd6a-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="0bd6a-613">Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="0bd6a-613">Spatial functions</span></span>       | <span data-ttu-id="0bd6a-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID e ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="0bd6a-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="0bd6a-615">Se attualmente si usa una funzione definita dall'utente (UDF) per cui è ora disponibile una funzione predefinita, è consigliabile usare la corrispondente funzione predefinita perché la sua esecuzione sarà più rapida ed efficiente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="0bd6a-616">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="0bd6a-616">Mathematical functions</span></span>
<span data-ttu-id="0bd6a-617">Le funzioni matematiche eseguono un calcolo basato su valori di input passati come argomenti e restituiscono un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="0bd6a-618">Di seguito è riportata una tabella delle funzioni matematiche predefinite supportate.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="0bd6a-619">Uso</span><span class="sxs-lookup"><span data-stu-id="0bd6a-619">Usage</span></span> | <span data-ttu-id="0bd6a-620">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0bd6a-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0bd6a-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="0bd6a-622">Restituisce il valore assoluto (positivo) dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="0bd6a-624">Restituisce il più piccolo valore integer maggiore di o uguale all'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="0bd6a-626">Restituisce il valore integer più alto, minore di o uguale all'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="0bd6a-628">Restituisce l'esponente dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="0bd6a-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="0bd6a-630">Restituisce il logaritmo naturale dell'espressione numerica specificata oppure il logaritmo usando la base specificata</span><span class="sxs-lookup"><span data-stu-id="0bd6a-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="0bd6a-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="0bd6a-632">Restituisce il valore logaritmico in base 10 dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="0bd6a-634">Restituisce un valore numerico, arrotondato al valore integer più vicino.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="0bd6a-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="0bd6a-636">Restituisce un valore numerico, troncato al valore integer più vicino.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="0bd6a-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="0bd6a-638">Restituisce la radica quadrata dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="0bd6a-640">Restituisce il quadrato dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="0bd6a-642">Restituisce la potenza dell'espressione numerica specificata al valore specificato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="0bd6a-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="0bd6a-644">Restituisce il valore del segno (-1, 0, 1) dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="0bd6a-646">Restituisce l'angolo, espresso in radianti, il cui coseno corrisponde all'espressione numerica specificata. Denominato anche arcocoseno.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="0bd6a-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="0bd6a-648">Restituisce l'angolo, espresso in radianti, il cui seno è l'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="0bd6a-649">Detta anche arcoseno.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="0bd6a-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="0bd6a-651">Restituisce l'angolo, espresso in radianti, la cui tangente è l'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="0bd6a-652">Detta anche arcotangente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="0bd6a-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="0bd6a-654">Restituisce l'angolo, espresso in radianti, tra l'asse x positivo e il raggio dall'origine al punto (y, x), dove x e y sono i valori delle due espressioni float specificate.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="0bd6a-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="0bd6a-656">Restituisce il coseno trigonometrico dell'angolo specificato, espresso in radianti, nell'espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="0bd6a-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="0bd6a-658">Restituisce la cotangente trigonometrica dell'angolo specificato, espresso in radianti, nell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="0bd6a-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="0bd6a-660">Restituisce l'angolo corrispondente in gradi di un angolo specificato in radianti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="0bd6a-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="0bd6a-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="0bd6a-662">Restituisce il valore costante di pi greco.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="0bd6a-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="0bd6a-664">Restituisce radianti quando viene immessa un'espressione numerica, espresso in gradi.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="0bd6a-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="0bd6a-666">Restituisce il seno trigonometrico dell'angolo specificato, espresso in radianti, nell'espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="0bd6a-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="0bd6a-668">Restituisce la tangente dell'espressione di input nell'espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="0bd6a-669">Ad esempio, è ora possibile eseguire query come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="0bd6a-670">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="0bd6a-671">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-671">**Results**</span></span>

    [4]

<span data-ttu-id="0bd6a-672">La differenza principale tra le funzioni di Cosmos DB rispetto ad ANSI SQL è che sono progettate per interagire correttamente con dati senza schema e con schema misto.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="0bd6a-673">Se ad esempio si ha un documento in cui manca la proprietà Size oppure caratterizzato da un valore non numerico, come "unknown", il documento viene ignorato invece di restituire un errore.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="0bd6a-674">Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="0bd6a-674">Type checking functions</span></span>
<span data-ttu-id="0bd6a-675">Le funzioni di controllo del tipo consentono di controllare il tipo di un'espressione nell'ambito delle query SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="0bd6a-676">Le funzioni di controllo del tipo possono essere usate per determinare il tipo di proprietà all'interno dei documenti al volo, quando è variabile o sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="0bd6a-677">Di seguito è riportata una tabella di funzioni predefinite di controllo del tipo supportate.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="0bd6a-678"><strong>Utilizzo</strong></span><span class="sxs-lookup"><span data-stu-id="0bd6a-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="0bd6a-679"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="0bd6a-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-681">Restituisce un valore booleano che indica se il tipo del valore è una matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-683">Restituisce un valore booleano che indica se il tipo del valore è booleano.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-685">Restituisce un valore booleano che indica se il tipo del valore è Null.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-687">Restituisce un valore booleano che indica se il tipo del valore è un numero.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-689">Restituisce un valore booleano che indica se il tipo del valore è un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-691">Restituisce un valore booleano che indica se il tipo del valore è una stringa.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-693">Restituisce un valore booleano che indica se alla proprietà è stata assegnato un valore.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="0bd6a-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="0bd6a-695">Restituisce un valore booleano che indica se il tipo del valore è stringa, numero, valore booleano o Null.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="0bd6a-696">Usando queste funzioni, è ora possibile eseguire query come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="0bd6a-697">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="0bd6a-698">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="0bd6a-699">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="0bd6a-699">String functions</span></span>
<span data-ttu-id="0bd6a-700">Le funzioni scalari seguenti eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, il valore numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="0bd6a-701">Ecco una tabella di funzioni per stringhe:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="0bd6a-702">Uso</span><span class="sxs-lookup"><span data-stu-id="0bd6a-702">Usage</span></span> | <span data-ttu-id="0bd6a-703">Description</span><span class="sxs-lookup"><span data-stu-id="0bd6a-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0bd6a-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="0bd6a-705">Restituisce il numero di caratteri dell'espressione stringa specificata</span><span class="sxs-lookup"><span data-stu-id="0bd6a-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="0bd6a-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="0bd6a-707">Restituisce una stringa che rappresenta il risultato della concatenazione di due o più valori di stringa.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="0bd6a-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="0bd6a-709">Restituisce parte di un'espressione stringa.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="0bd6a-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="0bd6a-711">Restituisce un valore booleano che indica se la prima espressione stringa termina con il secondo.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="0bd6a-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="0bd6a-713">Restituisce un valore booleano che indica se la prima espressione stringa termina con il secondo.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="0bd6a-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="0bd6a-715">Restituisce un valore booleano che indica se la prima espressione stringa contiene il secondo.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="0bd6a-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="0bd6a-717">Restituisce la posizione iniziale della prima occorrenza della seconda stringa di espressione all'interno della prima espressione stringa specificata oppure -1 se la stringa non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="0bd6a-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="0bd6a-719">Restituisce la parte sinistra di una stringa con il numero specificato di caratteri.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="0bd6a-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="0bd6a-721">Restituisce la parte destra di una stringa con il numero specificato di caratteri.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="0bd6a-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="0bd6a-723">Restituisce un'espressione stringa dopo aver rimosso gli spazi vuoti iniziali.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="0bd6a-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="0bd6a-725">Restituisce un'espressione stringa dopo la rimozione di tutti gli spazi vuoti finali.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="0bd6a-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="0bd6a-727">Restituisce un'espressione stringa dopo la conversione di dati in caratteri maiuscoli in caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="0bd6a-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="0bd6a-729">Restituisce un'espressione stringa dopo aver convertito i caratteri minuscoli in caratteri maiuscoli.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="0bd6a-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="0bd6a-731">Sostituisce tutte le occorrenze di un valore stringa specificato con un altro valore stringa.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="0bd6a-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="0bd6a-733">Ripete un valore stringa in un numero di volte specificato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="0bd6a-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="0bd6a-735">Restituisce l'inverso di un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="0bd6a-736">Usando queste funzioni, è ora possibile eseguire query come le seguenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="0bd6a-737">Ad esempio, è possibile restituire il nome della famiglia in lettere maiuscole come segue:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="0bd6a-738">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="0bd6a-739">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="0bd6a-740">In alternativa, è possibile concatenare stringhe come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="0bd6a-741">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="0bd6a-742">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="0bd6a-743">Le funzioni stringa possono essere usate anche nella clausola WHERE per filtrare i risultati, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="0bd6a-744">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="0bd6a-745">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="0bd6a-746">Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="0bd6a-746">Array functions</span></span>
<span data-ttu-id="0bd6a-747">Le funzioni scalari seguenti eseguono un'operazione su un valore di input di matrice e restituiscono un valore numerico, booleano o matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="0bd6a-748">La tabella seguente include funzioni di matrice predefinite:</span><span class="sxs-lookup"><span data-stu-id="0bd6a-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="0bd6a-749">Uso</span><span class="sxs-lookup"><span data-stu-id="0bd6a-749">Usage</span></span> | <span data-ttu-id="0bd6a-750">Description</span><span class="sxs-lookup"><span data-stu-id="0bd6a-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0bd6a-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="0bd6a-752">Restituisce il numero di elementi dell'espressione di matrice specificato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="0bd6a-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="0bd6a-754">Restituisce una matrice che rappresenta il risultato della concatenazione di due o più valori della matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="0bd6a-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="0bd6a-756">Restituisce un valore booleano che indica se la matrice contiene il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="0bd6a-757">Può specificare se la corrispondenza è completa o parziale.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="0bd6a-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="0bd6a-759">Restituisce parte di un'espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="0bd6a-760">Le funzioni di matrice possono essere usate per manipolare le matrici in JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="0bd6a-761">Ad esempio, la query seguente restituisce tutti i documenti in cui uno dei genitori è "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="0bd6a-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="0bd6a-762">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="0bd6a-763">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="0bd6a-764">È possibile specificare un frammento parziale per la corrispondenza di elementi all'interno della matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="0bd6a-765">La query seguente trova tutti gli elementi padre con `givenName` di `Robin`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="0bd6a-766">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="0bd6a-767">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="0bd6a-768">L'esempio seguente usa ARRAY_LENGTH per ottenere il numero di figli per ogni famiglia.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="0bd6a-769">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="0bd6a-770">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="0bd6a-771">Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="0bd6a-771">Spatial functions</span></span>
<span data-ttu-id="0bd6a-772">Cosmos DB supporta le seguenti funzioni predefinite di Open Geospatial Consortium (OGC) per l'esecuzione di query geospaziali.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="0bd6a-773"><strong>Utilizzo</strong></span><span class="sxs-lookup"><span data-stu-id="0bd6a-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="0bd6a-774"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="0bd6a-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="0bd6a-776">Restituisce la distanza tra le due espressioni GeoJSON punto, poligono o LineString.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="0bd6a-778">Restituisce un'espressione booleana che indica se il primo oggetto GeoJSON (punto, poligono o LineString) è all'interno del secondo oggetto GeoJSON (punto, poligono o LineString).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="0bd6a-780">Restituisce un'espressione booleana che indica se i due oggetti GeoJSON specificati (punto, poligono o LineString) si intersecano.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="0bd6a-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="0bd6a-782">Restituisce un valore booleano che indica se l'espressione GeoJSON punto, poligono o LineString specificata è valida.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="0bd6a-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="0bd6a-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="0bd6a-784">Restituisce un valore JSON che contiene un valore booleano valore se l'espressione GeoJSON punto, poligono o LineString specificata è valida e, se non valida, anche il motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="0bd6a-785">Le funzioni spaziali possono essere utilizzate per eseguire query di prossimità rispetto ai dati spaziali.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="0bd6a-786">Ad esempio, di seguito è riportata una query che restituisce tutti i documenti della famiglia entro 30 km della posizione specificata utilizzando la funzione predefinita ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="0bd6a-787">**Query**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="0bd6a-788">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="0bd6a-789">Per informazioni dettagliate sul supporto geospaziale in Cosmos DB, vedere [Uso dei dati geospaziali in Azure Cosmos DB](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="0bd6a-790">Viene eseguito il wrapping di funzioni spaziali e della sintassi SQL per Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="0bd6a-791">Verrà ora esaminato il funzionamento delle query LINQ e verrà illustrato il modo in cui interagiscono con la sintassi esaminata fino ad ora.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="0bd6a-792"><a id="Linq"></a>Da LINQ all'API SQL di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0bd6a-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="0bd6a-793">LINQ è un modello di programmazione .NET che esprime il calcolo come query su flussi di oggetti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="0bd6a-794">Cosmos DB fornisce una libreria lato client che si interfaccia con LINQ agevolando una conversione tra oggetti JSON e .NET e un mapping da un sottoinsieme di query LINQ alle query di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="0bd6a-795">L'immagine seguente illustra l'architettura di supporto delle query LINQ usando Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="0bd6a-796">Con il client di Cosmos DB, gli sviluppatori possono creare un oggetto **IQueryable** che comunica una query al provider di query di Cosmos DB, il quale a sua volta traduce la query LINQ in una query di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="0bd6a-797">Questa viene quindi passata al server di Cosmos DB per recuperare un set di risultati in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="0bd6a-798">I risultati restituiti vengono deserializzati in un flusso di oggetti .NET sul lato client.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Architettura di supporto delle query LINQ usando API DocumentDB - Sintassi SQL, linguaggio di query JSON, concetti relativi ai database e query SQL][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="0bd6a-800">Mapping .NET e JSON</span><span class="sxs-lookup"><span data-stu-id="0bd6a-800">.NET and JSON mapping</span></span>
<span data-ttu-id="0bd6a-801">Il mapping tra oggetti .NET e documenti JSON avviene naturalmente: ogni campo del membro dati viene mappato a un oggetto JSON, in cui il nome del campo viene mappato alla parte "chiave" dell'oggetto e la parte "valore" viene mappata in modo ricorsivo alla parte del valore dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="0bd6a-802">Si consideri l'esempio seguente: l'oggetto Family creato viene mappato al documento JSON, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="0bd6a-803">Viceversa, il documento JSON viene mappato nuovamente a un oggetto .NET.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="0bd6a-804">**Classe C#**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-804">**C# Class**</span></span>

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


<span data-ttu-id="0bd6a-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-805">**JSON**</span></span>  

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



### <a name="linq-to-sql-translation"></a><span data-ttu-id="0bd6a-806">Traduzione LINQ in SQL</span><span class="sxs-lookup"><span data-stu-id="0bd6a-806">LINQ to SQL translation</span></span>
<span data-ttu-id="0bd6a-807">Il provider di query di Cosmos DB esegue con il massimo impegno un mapping da una query LINQ a una query SQL di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="0bd6a-808">Nella descrizione seguente si presuppone che il lettore abbia una certa familiarità con LINQ.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="0bd6a-809">In primo luogo, per il sistema di tipi sono supportati tutti i tipi primitivi JSON: tipi numerici, booleani, stringa e null.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="0bd6a-810">Sono supportati solo questi tipi JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-810">Only these JSON types are supported.</span></span> <span data-ttu-id="0bd6a-811">Sono supportate le seguenti espressioni scalari.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="0bd6a-812">Valori costanti: includono i valori costanti dei tipo di dati primitivi al momento della valutazione della query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="0bd6a-813">Espressioni indice della matrice/di proprietà: queste espressioni si riferiscono alla proprietà di un oggetto o di un elemento matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="0bd6a-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n è una variabile di tipo int</span><span class="sxs-lookup"><span data-stu-id="0bd6a-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="0bd6a-815">Espressioni aritmetiche: includono espressioni aritmetiche comuni su valori numerici e booleani.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="0bd6a-816">Per un elenco completo, fare riferimento alle specifiche di SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="0bd6a-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="0bd6a-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="0bd6a-818">Espressione di confronto stringhe: includono il confronto di un valore di stringa con un valore di stringa costante.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="0bd6a-819">mother.familyName == "Smith";    child.givenName == s; //s è una variabile di stringa</span><span class="sxs-lookup"><span data-stu-id="0bd6a-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="0bd6a-820">Espressione di creazione oggetto/matrice: restituisce un oggetto di tipo valore composito o tipo anonimo o ancora un matrice di tali oggetti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="0bd6a-821">Questi valori non possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-821">These values can be nested.</span></span>
  
     <span data-ttu-id="0bd6a-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //un tipo anonimo con due campi</span><span class="sxs-lookup"><span data-stu-id="0bd6a-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="0bd6a-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="0bd6a-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="0bd6a-824"><a id="SupportedLinqOperators"></a>Elenco di operatori LINQ supportati</span><span class="sxs-lookup"><span data-stu-id="0bd6a-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="0bd6a-825">Di seguito è riportato un elenco di operatori LINQ supportati nel provider LINQ incluso in DocumentDB .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="0bd6a-826">**Select**: le proiezioni convertono in SQL SELECT inclusa la costruzione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="0bd6a-827">**Where**: i filtri convertono in SQL WHERE e supportano la conversione tra && , || e !</span><span class="sxs-lookup"><span data-stu-id="0bd6a-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="0bd6a-828">in operatori SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-828">to the SQL operators</span></span>
* <span data-ttu-id="0bd6a-829">**SelectMany**: consente la rimozione di matrici nella clausola SQL JOIN.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="0bd6a-830">Può essere usato per concatenare/annidare le espressioni per filtrare in base agli elementi della matrice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="0bd6a-831">**OrderBy e OrderByDescending**: converte in ORDER BY crescente o decrescente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="0bd6a-832">Operatori di aggregazione **Count**, **Sum**, **Min**, **Max** e **Average** e relativi equivalenti asincroni **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** e **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="0bd6a-833">**CompareTo**: converte in confronti di intervallo.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="0bd6a-834">In genere usato per le stringhe in quanto non sono confrontabili in .NET</span><span class="sxs-lookup"><span data-stu-id="0bd6a-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="0bd6a-835">**Take**: converte in SQL TOP per limitare i risultati da una query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="0bd6a-836">**Math Functions**: supporta la conversione da Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan e Truncate di .NET nelle funzioni predefinite di SQL equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="0bd6a-837">**String Functions**: supporta la conversione da Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString e ToUpper di .NET nelle funzioni predefinite di SQL equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="0bd6a-838">**Array Functions**: supporta la conversione da Concat, Contains e Count di .NET nelle funzioni predefinite di SQL equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="0bd6a-839">**Geospatial Extension Functions**: supporta la conversione dai metodi sthub Distance, Within, IsValid e IsValidDetailed nelle funzioni predefinite di SQL equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="0bd6a-840">**User Defined Function Extension Function**: supporta la conversione dal metodo stub UserDefinedFunctionProvider.Invoke alla funzione corrispondente definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="0bd6a-841">**Miscellaneous**: supporta la conversione degli operatori condizionali e di unione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="0bd6a-842">Consente la conversione di Contains in String CONTAINS, ARRAY_CONTAINS o SQL IN in base al contesto.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="0bd6a-843">Operatori di query SQL</span><span class="sxs-lookup"><span data-stu-id="0bd6a-843">SQL query operators</span></span>
<span data-ttu-id="0bd6a-844">Di seguito sono riportati alcuni esempi che illustrano in che modo gli operatori di query LINQ standard vengono tradotti in query di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="0bd6a-845">Operatore Select</span><span class="sxs-lookup"><span data-stu-id="0bd6a-845">Select Operator</span></span>
<span data-ttu-id="0bd6a-846">La sintassi è `input.Select(x => f(x))`, dove `f` è un'espressione scalare.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="0bd6a-847">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="0bd6a-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="0bd6a-849">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="0bd6a-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="0bd6a-851">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="0bd6a-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="0bd6a-853">Operatore SelectMany</span><span class="sxs-lookup"><span data-stu-id="0bd6a-853">SelectMany operator</span></span>
<span data-ttu-id="0bd6a-854">La sintassi è `input.SelectMany(x => f(x))`, dove `f` è un'espressione scalare che restituisce un tipo di raccolta.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="0bd6a-855">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="0bd6a-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="0bd6a-857">Operatore Where</span><span class="sxs-lookup"><span data-stu-id="0bd6a-857">Where operator</span></span>
<span data-ttu-id="0bd6a-858">La sintassi è `input.Where(x => f(x))`, dove `f` è un'espressione scalare che restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="0bd6a-859">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="0bd6a-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="0bd6a-861">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="0bd6a-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="0bd6a-863">Query SQL composte</span><span class="sxs-lookup"><span data-stu-id="0bd6a-863">Composite SQL queries</span></span>
<span data-ttu-id="0bd6a-864">Gli operatori sopra riportati possono essere composti in modo da formare query più potenti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="0bd6a-865">Poiché Cosmos DB supporta raccolte nidificate, la composizione può essere concatenata o annidata.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="0bd6a-866">Concatenazione</span><span class="sxs-lookup"><span data-stu-id="0bd6a-866">Concatenation</span></span>
<span data-ttu-id="0bd6a-867">La sintassi è `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="0bd6a-868">Una query concatenata può iniziare con una query `SelectMany` facoltativa, seguita da più operatori `Select` o `Where`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="0bd6a-869">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="0bd6a-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="0bd6a-871">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="0bd6a-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="0bd6a-873">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="0bd6a-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="0bd6a-875">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="0bd6a-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="0bd6a-877">Annidamento</span><span class="sxs-lookup"><span data-stu-id="0bd6a-877">Nesting</span></span>
<span data-ttu-id="0bd6a-878">La sintassi è `input.SelectMany(x=>x.Q())` dove Q è un operatore `Select`, `SelectMany` o `Where`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="0bd6a-879">In una query annidata, la query più interna viene applicata a ogni elemento della raccolta esterna.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="0bd6a-880">Una funzionalità importante è che la query interna può riferirsi ai campi degli elementi nella raccolta esterna come a self-join.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="0bd6a-881">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="0bd6a-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="0bd6a-883">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="0bd6a-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="0bd6a-885">**Espressione lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="0bd6a-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="0bd6a-887"><a id="ExecutingSqlQueries"></a>Esecuzione di query SQL</span><span class="sxs-lookup"><span data-stu-id="0bd6a-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="0bd6a-888">Cosmos DB espone risorse tramite un'API REST che può essere chiamata da qualsiasi linguaggio in grado di effettuare richieste HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="0bd6a-889">In Cosmos DB sono anche disponibili librerie di programmazione per diversi linguaggi comuni, come NET, Node.js, JavaScript e Python.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="0bd6a-890">L'API REST e le varie librerie supportano tutte l'esecuzione di query tramite SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="0bd6a-891">.NET SDK supporta l'esecuzione di query LINQ oltre a SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="0bd6a-892">Negli esempi seguenti viene illustrato come creare una query e inviarla a fronte di un account di database di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="0bd6a-893"><a id="RestAPI"></a>API REST</span><span class="sxs-lookup"><span data-stu-id="0bd6a-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="0bd6a-894">Cosmos DB offre un modello di programmazione aperto RESTful su HTTP.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="0bd6a-895">È possibile effettuare il provisioning degli account di database usando una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="0bd6a-896">Il modello di risorse di Cosmos DB è costituito da un set di risorse disponibili in un account di database e indirizzabili singolarmente tramite un URI logico e stabile.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="0bd6a-897">Un insieme di risorse viene definito feed nel presente documento.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="0bd6a-898">Un account di database è costituito da un set di database, ognuno dei quali include più raccolte, che possono contenere documenti, UDF e altri tipi di risorse.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="0bd6a-899">Il modello di interazione di base con queste risorse usa i verbi HTTP GET, PUT, POST e DELETE con la relativa interpretazione standard.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="0bd6a-900">Il verbo POST viene usato per creare una nuova risorsa, per eseguire una stored procedure o per inviare una query di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="0bd6a-901">Le query sono sempre operazioni di sola lettura senza nessun effetto collaterale.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="0bd6a-902">Gli esempi seguenti illustrano un'azione POST per una query dell'API di DocumentDB a fronte di una raccolta contenente i due documenti di esempio esaminati finora.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="0bd6a-903">La query ha un semplice filtro sulla proprietà nome JSON.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="0bd6a-904">Si noti l'uso delle intestazioni `x-ms-documentdb-isquery` e Content-Type `application/query+json` per indicare che l'operazione è una query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="0bd6a-905">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-905">**Request**</span></span>

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


<span data-ttu-id="0bd6a-906">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-906">**Results**</span></span>

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


<span data-ttu-id="0bd6a-907">Il secondo esempio mostra una query più complessa che restituisce più risultati dal join.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="0bd6a-908">**Richiesta**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-908">**Request**</span></span>

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


<span data-ttu-id="0bd6a-909">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="0bd6a-909">**Results**</span></span>

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


<span data-ttu-id="0bd6a-910">Se il numero di risultati di una query supera le dimensioni di una singola pagina, l'API REST restituisce un token di continuazione attraverso l'intestazione di risposta `x-ms-continuation-token` .</span><span class="sxs-lookup"><span data-stu-id="0bd6a-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="0bd6a-911">I client possono impaginare i risultati includendo l'intestazione nei risultati successivi.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="0bd6a-912">È possibile controllare il numero di risultati per pagina anche attraverso l'intestazione di numero `x-ms-max-item-count` .</span><span class="sxs-lookup"><span data-stu-id="0bd6a-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="0bd6a-913">Se la query specificata include una funzione di aggregazione come `COUNT`, la pagina di query può restituire un valore parzialmente aggregato nella pagina dei risultati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="0bd6a-914">I client devono eseguire un'aggregazione di secondo livello su questi risultati per ottenere i risultati finali, ad esempio sommare i conteggi restituiti nelle singole pagine per ottenere il conteggio totale.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="0bd6a-915">Per gestire i criteri di coerenza dei dati per le query, usare l'intestazione `x-ms-consistency-level` come tutte le richieste dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="0bd6a-916">Ai fini della coerenza della sessione, è necessario anche ripetere l'ultima intestazione cookie `x-ms-session-token` nella richiesta di query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="0bd6a-917">I criteri di indicizzazione della raccolta sulla quale è stata eseguita la query possono influenzare anche la coerenza dei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="0bd6a-918">Con le impostazioni predefinite dei criteri di indicizzazione, per le raccolte l'indice è sempre aggiornato con il contenuto del documento e i risultati della query corrispondono alla coerenza scelta per i dati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="0bd6a-919">Se i criteri di indicizzazione vengono ridotti alla modalità differita, le query possono restituire risultati obsoleti.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="0bd6a-920">Per altre informazioni, vedere [Livelli di coerenza di Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="0bd6a-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="0bd6a-921">Se i criteri di indicizzazione configurati sulla raccolta non possono supportare la query specificata, il server di Azure Cosmos DB restituisce il codice di errore 400 (Richiesta non valida).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="0bd6a-922">Questo codice viene restituito per le query di intervallo per ricerche hash (uguaglianza) e per i percorsi esplicitamente esclusi dall'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="0bd6a-923">È possibile specificare l'intestazione `x-ms-documentdb-query-enable-scan` per consentire alla query di eseguire una scansione quando non è disponibile un indice.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="0bd6a-924">È possibile ottenere metriche dettagliate sull'esecuzione di query impostando l'intestazione `x-ms-documentdb-populatequerymetrics` su `True`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="0bd6a-925">Per altre informazioni, vedere [metriche di query SQL per l'API Azure Cosmos DB DocumentDB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="0bd6a-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="0bd6a-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="0bd6a-927">.NET SDK supporta l'esecuzione di query LINQ ed SQL.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="0bd6a-928">Nell'esempio seguente viene illustrato come eseguire la semplice query di filtro introdotta in precedenza in questo documento.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="0bd6a-929">In questo esempio vengono confrontate due proprietà per l'uguaglianza all'interno di ciascun documento, usando le proiezioni anonime.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="0bd6a-930">Nell'esempio successivo vengono illustrati i join, espressi tramite la clausola SelectMany di LINQ.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="0bd6a-931">Il client .NET esegue automaticamente l'iterazione attraverso tutte le pagine dei risultati della query nei blocchi foreach, come sopra illustrato.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="0bd6a-932">Le opzioni di query presentate nella sezione dell'API REST sono disponibili anche in .NET SDK usando le classi `FeedOptions` and `FeedResponse` nel metodo CreateDocumentQuery.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="0bd6a-933">È possibile controllare il numero di pagine usando l'impostazione `MaxItemCount` .</span><span class="sxs-lookup"><span data-stu-id="0bd6a-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="0bd6a-934">È anche possibile controllare esplicitamente il paging creando `IDocumentQueryable` tramite l'oggetto `IQueryable`, quindi leggendo i valori ` ResponseContinuationToken` e ritrasferendoli come `RequestContinuationToken` in `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="0bd6a-935">`EnableScanInQuery` per abilitare le analisi quando la query non può essere supportata dai criteri di indicizzazione configurati.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="0bd6a-936">Per le raccolte partizionate, è possibile usare `PartitionKey` per eseguire la query in una partizione singola, anche se Cosmos DB può eseguire l'estrazione automatica dal testo della query, e `EnableCrossPartitionQuery` per eseguire query che potrebbe essere necessario ripetere in più partizioni.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="0bd6a-937">Per altri esempi contenenti query, vedere gli [esempi relativi a .NET in Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net).</span><span class="sxs-lookup"><span data-stu-id="0bd6a-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="0bd6a-938"><a id="JavaScriptServerSideApi"></a>API lato server JavaScript</span><span class="sxs-lookup"><span data-stu-id="0bd6a-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="0bd6a-939">Cosmos DB offre un modello di programmazione per l'esecuzione di logica dell'applicazione basata su JavaScript direttamente nelle raccolte usando stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="0bd6a-940">La logica JavaScript registrata a livello di raccolta può quindi rilasciare operazioni sui documenti della raccolta specifica.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="0bd6a-941">Viene quindi eseguito il wrapping di queste operazioni nelle transazioni ACID Ambient.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="0bd6a-942">L'esempio seguente mostra come usare queryDocuments nell'API del server JavaScript per eseguire query dall'interno di stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

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

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="0bd6a-943"><a id="References"></a>Riferimenti</span><span class="sxs-lookup"><span data-stu-id="0bd6a-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="0bd6a-944">[Introduzione ad Azure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="0bd6a-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="0bd6a-945">Specifica SQL di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0bd6a-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="0bd6a-946">Esempi relativi a Azure Cosmos DB .NET</span><span class="sxs-lookup"><span data-stu-id="0bd6a-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="0bd6a-947">[Livelli di coerenza di Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="0bd6a-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="0bd6a-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="0bd6a-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="0bd6a-950">Specifiche Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="0bd6a-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="0bd6a-952">Tecniche di valutazione delle query per database di grandi dimensioni [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="0bd6a-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="0bd6a-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="0bd6a-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="0bd6a-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="0bd6a-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: un linguaggio non così estraneo per l'elaborazione dati, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="0bd6a-956">G.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-956">G.</span></span> <span data-ttu-id="0bd6a-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-957">Graefe.</span></span> <span data-ttu-id="0bd6a-958">The Cascades framework for query optimization.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="0bd6a-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-959">IEEE Data Eng.</span></span> <span data-ttu-id="0bd6a-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="0bd6a-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md