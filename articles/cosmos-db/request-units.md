---
title: "Unità richiesta e stima della velocità effettiva: Azure Cosmos DB | Microsoft Docs"
description: "Informazioni su come comprendere, specificare e stimare i requisiti relativi alle unità richiesta in Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7a4efc0fb9b3855b9dbbe445768ceb2a9940d0b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="85b5d-103">Unità richiesta in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85b5d-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="85b5d-104">Ora disponibile: [calcolatore di unità richiesta](https://www.documentdb.com/capacityplanner) di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85b5d-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="85b5d-105">Per altre informazioni, vedere [Stima delle esigenze di velocità effettiva](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="85b5d-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Calcolatore della velocità effettiva][5]

## <a name="introduction"></a><span data-ttu-id="85b5d-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="85b5d-107">Introduction</span></span>
<span data-ttu-id="85b5d-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) è il database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="85b5d-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="85b5d-109">Con Azure Cosmos DB non è necessario affittare macchine virtuali, distribuire software o monitorare database.</span><span class="sxs-lookup"><span data-stu-id="85b5d-109">With Azure Cosmos DB, you don't have to rent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="85b5d-110">Azure Cosmos DB è gestito e monitorato costantemente dai migliori tecnici Microsoft, in modo da offrire disponibilità, prestazioni e protezione dei dati di elevata qualità.</span><span class="sxs-lookup"><span data-stu-id="85b5d-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers to deliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="85b5d-111">Permette di accedere ai dati usando le API preferite, perché supporta in modalità nativa [SQL di DocumentDB](documentdb-sql-query.md) (documenti), MongoDB (documenti), [Archiviazione tabelle di Azure](https://azure.microsoft.com/services/storage/tables/) (chiave-valore) e [Gremlin](https://tinkerpop.apache.org/gremlin.html) (grafi).</span><span class="sxs-lookup"><span data-stu-id="85b5d-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="85b5d-112">La valuta di Azure Cosmos DB è costituita dalle unità richiesta (UR).</span><span class="sxs-lookup"><span data-stu-id="85b5d-112">The currency of Azure Cosmos DB is the Request Unit (RU).</span></span> <span data-ttu-id="85b5d-113">Con le unità richiesta, non è necessario riservare capacità di lettura/scrittura né effettuare il provisioning di CPU, memoria e operazioni di I/O al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-113">With RUs, you do not need to reserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="85b5d-114">Azure Cosmos DB supporta una serie di API con operazioni diverse, che vanno dalla semplice lettura e scrittura alle query per grafi più complesse.</span><span class="sxs-lookup"><span data-stu-id="85b5d-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes to complex graph queries.</span></span> <span data-ttu-id="85b5d-115">Poiché non tutte le richieste sono uguali, viene loro assegnata una quantità normalizzata di **unità richiesta** in base alla quantità di calcolo necessaria per servire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on the amount of computation required to serve the request.</span></span> <span data-ttu-id="85b5d-116">Il numero di unità richiesta per un'operazione è deterministico ed è possibile tenere traccia del numero di unità richiesta utilizzate da qualsiasi operazione in Azure Cosmos DB tramite un'intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="85b5d-117">Per prestazioni prevedibili, è necessario riservare una velocità effettiva in unità di 100 UR/secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-117">To provide predictable performance, you need to reserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="85b5d-118">Alla fine della lettura, si avranno le risposte alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="85b5d-118">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="85b5d-119">Cosa sono le unità richiesta e gli addebiti richiesta?</span><span class="sxs-lookup"><span data-stu-id="85b5d-119">What are request units and request charges?</span></span>
* <span data-ttu-id="85b5d-120">Come è possibile specificare la capacità delle unità richiesta per una raccolta?</span><span class="sxs-lookup"><span data-stu-id="85b5d-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="85b5d-121">Come si possono stimare le esigenze relative alle unità richiesta per l'applicazione?</span><span class="sxs-lookup"><span data-stu-id="85b5d-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="85b5d-122">Cosa accade se si supera la capacità delle unità richiesta per una raccolta?</span><span class="sxs-lookup"><span data-stu-id="85b5d-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="85b5d-123">Azure Cosmos DB è un database multimodello. Si noti che in questo articolo l'API di documento è detta raccolta/documento, l'API Graph è detta grafo/nodo e l'API di tabella è detta tabella/entità.</span><span class="sxs-lookup"><span data-stu-id="85b5d-123">As Azure Cosmos DB is a multi-model database, it is important to note that we will refer to a collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="85b5d-124">Per la velocità effettiva nell'articolo vengono usati i concetti generali di contenitore/elemento.</span><span class="sxs-lookup"><span data-stu-id="85b5d-124">Throughput this document we will generalize to the concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="85b5d-125">Unità richiesta e addebiti richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-125">Request units and request charges</span></span>
<span data-ttu-id="85b5d-126">Azure Cosmos DB offre prestazioni veloci e prevedibili, *riservando* risorse per soddisfare le esigenze a livello di velocità effettiva dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85b5d-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span></span>  <span data-ttu-id="85b5d-127">Poiché i modelli di carico e accesso dell'applicazione cambiano nel tempo, Azure Cosmos DB consente di aumentare o diminuire facilmente la quantità di velocità effettiva riservata disponibile per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85b5d-127">Because application load and access patterns change over time, Azure Cosmos DB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span></span>

<span data-ttu-id="85b5d-128">Con Azure Cosmos DB, la velocità effettiva riservata è specificata in termini di unità richiesta elaborate al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="85b5d-129">Si possono considerare le unità richiesta come una specie di valuta della velocità effettiva, secondo cui si *riserva* una quantità garantita di unità richiesta disponibili al secondo per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85b5d-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span></span>  <span data-ttu-id="85b5d-130">Ogni operazione in Azure Cosmos DB, ovvero scrittura di un documento, esecuzione di una query, aggiornamento di un documento, utilizza CPU, memoria e operazioni di I/O al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="85b5d-131">In altre parole, ogni operazione comporta un *addebito richiesta* espresso in *unità richiesta*.</span><span class="sxs-lookup"><span data-stu-id="85b5d-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="85b5d-132">La conoscenza dei fattori che influiscono sugli addebiti delle unità richiesta, insieme ai requisiti di velocità effettiva dell'applicazione, consente di eseguire l'applicazione nel modo più economicamente conveniente possibile.</span><span class="sxs-lookup"><span data-stu-id="85b5d-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span></span> <span data-ttu-id="85b5d-133">Anche lo strumento Esplora query è molto utile per testare gli elementi di base di una query.</span><span class="sxs-lookup"><span data-stu-id="85b5d-133">The query explorer is also a wonderful tool to test the core of a query.</span></span>

<span data-ttu-id="85b5d-134">Per iniziare è consigliabile guardare il video riportato di seguito, in cui Aravind Ramachandran illustra le unità richiesta e le prestazioni prevedibili con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85b5d-134">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="85b5d-135">Specifica della capacità in unità richiesta in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85b5d-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="85b5d-136">Quando si crea una nuova raccolta, tabella o grafo, si specifica il numero di unità richiesta al secondo (UR/sec) da riservare.</span><span class="sxs-lookup"><span data-stu-id="85b5d-136">When starting a new collection, table or graph, you specify the number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="85b5d-137">In base alla velocità effettiva di cui è stato effettuato il provisioning, Azure Cosmos DB alloca partizioni fisiche per ospitare la raccolta e suddivide/ribilancia la crescita dei dati nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="85b5d-137">Based on the provisioned throughput, Azure Cosmos DB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="85b5d-138">In Azure Cosmos DB è necessario specificare una chiave di partizione quando viene effettuato il provisioning di una raccolta con almeno 2.500 unità richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-138">Azure Cosmos DB requires a partition key to be specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="85b5d-139">La chiave di partizione è necessaria anche per ridimensionare la velocità effettiva della raccolta oltre le 2.500 unità richiesta in futuro.</span><span class="sxs-lookup"><span data-stu-id="85b5d-139">A partition key is also required to scale your collection's throughput beyond 2,500 request units in the future.</span></span> <span data-ttu-id="85b5d-140">È quindi consigliabile configurare una [chiave di partizione](partition-data.md) durante la creazione di un contenitore, indipendentemente dalla velocità effettiva iniziale.</span><span class="sxs-lookup"><span data-stu-id="85b5d-140">Therefore, it is highly recommended to configure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="85b5d-141">Dato che potrebbe essere necessario suddividere i dati in più partizioni, occorre scegliere una chiave di partizione con una cardinalità elevata, da centinaia a milioni di valori distinti, in modo che Azure Cosmos DB possa ridimensionare la raccolta, la tabella o il grafo e le richieste in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="85b5d-141">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="85b5d-142">Una chiave di partizione è un limite logico, non un limite fisico.</span><span class="sxs-lookup"><span data-stu-id="85b5d-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="85b5d-143">Non è quindi necessario limitare il numero di valori distinti per le chiavi di partizioni.</span><span class="sxs-lookup"><span data-stu-id="85b5d-143">Therefore, you do not need to limit the number of distinct partition key values.</span></span> <span data-ttu-id="85b5d-144">È in effetti consigliabile avere un numero maggiore di valori distinti per le chiavi di partizione, perché Azure Cosmos DB offre un numero maggiore di opzioni per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="85b5d-144">It is in fact better to have more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="85b5d-145">Ecco un frammento di codice per la creazione di una raccolta con 3.000 unità richiesta al secondo usando .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="85b5d-145">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="85b5d-146">Azure Cosmos DB usa un modello di prenotazione per la velocità effettiva,</span><span class="sxs-lookup"><span data-stu-id="85b5d-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="85b5d-147">ovvero viene fatturata la quantità di velocità effettiva *riservata*, indipendentemente dalla quantità di tale velocità effettiva *usata* attivamente.</span><span class="sxs-lookup"><span data-stu-id="85b5d-147">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="85b5d-148">A mano a mano che i modelli di carico, dati e utilizzo dell'applicazione cambiano, è possibile aumentare e ridurre facilmente la quantità di unità richiesta riservate usando gli SDK o il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85b5d-148">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="85b5d-149">Viene eseguito il mapping di ogni raccolta, tabella o grafo a una risorsa `Offer` in Azure Cosmos DB, che include metadati sulla velocità effettiva di cui è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="85b5d-149">Each collection/table/graph are mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span></span> <span data-ttu-id="85b5d-150">È possibile modificare la velocità effettiva allocata esaminando l'offerta corrispondente relativa alla risorsa per un contenitore, quindi aggiornarla con il nuovo valore per la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="85b5d-150">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span></span> <span data-ttu-id="85b5d-151">Ecco un frammento di codice per la modifica della velocità effettiva di una raccolta fino a 5.000 unità richiesta al secondo usando .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="85b5d-151">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span></span>

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="85b5d-152">La modifica della velocità effettiva non influisce sulla disponibilità del contenitore.</span><span class="sxs-lookup"><span data-stu-id="85b5d-152">There is no impact to the availability of your container when you change the throughput.</span></span> <span data-ttu-id="85b5d-153">La nuova velocità effettiva riservata viene in genere applicata entro pochi secondi, in corrispondenza dell'applicazione della nuova velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="85b5d-153">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="85b5d-154">Considerazioni sulle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-154">Request unit considerations</span></span>
<span data-ttu-id="85b5d-155">Quando si stima il numero di unità richiesta da riservare per il contenitore di Azure Cosmos DB, è importante considerare le variabili seguenti:</span><span class="sxs-lookup"><span data-stu-id="85b5d-155">When estimating the number of request units to reserve for your Azure Cosmos DB container, it is important to take the following variables into consideration:</span></span>

* <span data-ttu-id="85b5d-156">**Dimensioni dell'elemento**.</span><span class="sxs-lookup"><span data-stu-id="85b5d-156">**Item size**.</span></span> <span data-ttu-id="85b5d-157">Con l'aumento delle dimensioni aumentano anche le unità utilizzate per leggere o scrivere i dati.</span><span class="sxs-lookup"><span data-stu-id="85b5d-157">As size increases the units consumed to read or write the data will also increase.</span></span>
* <span data-ttu-id="85b5d-158">**Numero di proprietà dell'elemento**.</span><span class="sxs-lookup"><span data-stu-id="85b5d-158">**Item property count**.</span></span> <span data-ttu-id="85b5d-159">Presupponendo l'indicizzazione predefinita di tutte le proprietà, le unità utilizzate per scrivere un documento, un nodo o un'entità aumentano con l'aumento del numero delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="85b5d-159">Assuming default indexing of all properties, the units consumed to write a document/node/ntity will increase as the property count increases.</span></span>
* <span data-ttu-id="85b5d-160">**Coerenza dei dati**.</span><span class="sxs-lookup"><span data-stu-id="85b5d-160">**Data consistency**.</span></span> <span data-ttu-id="85b5d-161">Se si usano i livelli di coerenza dei dati Assoluta o Con obsolescenza associata, verranno utilizzate ulteriori unità per leggere gli elementi.</span><span class="sxs-lookup"><span data-stu-id="85b5d-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read items.</span></span>
* <span data-ttu-id="85b5d-162">**Proprietà indicizzate**.</span><span class="sxs-lookup"><span data-stu-id="85b5d-162">**Indexed properties**.</span></span> <span data-ttu-id="85b5d-163">I criteri di indicizzazione in ogni contenitore determinano le proprietà che vengono indicizzate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="85b5d-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="85b5d-164">È possibile ridurre l'utilizzo di unità richiesta limitando il numero di proprietà indicizzate o abilitando l'indicizzazione differita.</span><span class="sxs-lookup"><span data-stu-id="85b5d-164">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="85b5d-165">**Indicizzazione del documento**.</span><span class="sxs-lookup"><span data-stu-id="85b5d-165">**Document indexing**.</span></span> <span data-ttu-id="85b5d-166">Per impostazione predefinita ogni elemento viene indicizzato automaticamente, ma se si sceglie di non indicizzare alcuni elementi si utilizzeranno meno unità di richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-166">By default each item is automatically indexed, you will consume fewer request units if you choose not to index some of your items.</span></span>
* <span data-ttu-id="85b5d-167">**Modelli di query**.</span><span class="sxs-lookup"><span data-stu-id="85b5d-167">**Query patterns**.</span></span> <span data-ttu-id="85b5d-168">La complessità di una query influisce sulla quantità di unità richiesta utilizzate per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="85b5d-168">The complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="85b5d-169">Il numero di predicati, la natura dei predicati, le proiezioni, il numero di funzioni definite dall'utente e le dimensioni del set di dati di origine sono tutti fattori che incidono sul costo delle operazioni di query.</span><span class="sxs-lookup"><span data-stu-id="85b5d-169">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span></span>
* <span data-ttu-id="85b5d-170">**Utilizzo di script**.</span><span class="sxs-lookup"><span data-stu-id="85b5d-170">**Script usage**.</span></span>  <span data-ttu-id="85b5d-171">Come le query, le stored procedure e i trigger utilizzano le unità richiesta in base alla complessità delle operazioni da eseguire.</span><span class="sxs-lookup"><span data-stu-id="85b5d-171">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span></span> <span data-ttu-id="85b5d-172">Quando si sviluppa l'applicazione, controllare l'intestazione per l'addebito delle richieste per comprendere meglio il modo in cui ciascuna operazione usa la capacità delle unità di richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-172">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="85b5d-173">Stima delle esigenze di velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="85b5d-173">Estimating throughput needs</span></span>
<span data-ttu-id="85b5d-174">Un'unità di richiesta è una misura normalizzata del costo di elaborazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="85b5d-175">Una singola unità richiesta rappresenta la capacità di elaborazione necessaria per leggere, tramite collegamento automatico o ID, un singolo elemento da 1 KB costituito da 10 valori di proprietà univoci, escluse le proprietà di sistema.</span><span class="sxs-lookup"><span data-stu-id="85b5d-175">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="85b5d-176">Una richiesta di creazione (inserimento), sostituzione o eliminazione dello stesso elemento utilizzerà più capacità di elaborazione del servizio e quindi più unità richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-176">A request to create (insert), replace or delete the same item will consume more processing from the service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="85b5d-177">La base di 1 unità richiesta per un elemento da 1 KB corrisponde a una semplice operazione GET tramite collegamento automatico o ID dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="85b5d-177">The baseline of 1 request unit for a 1KB item corresponds to a simple GET by self link or id of the item.</span></span>
> 
> 

<span data-ttu-id="85b5d-178">La tabella riportata di seguito mostra il numero di unità richiesta di cui effettuare il provisioning per tre dimensioni dell'elemento diverse, ovvero 1 KB, 4 KB e 64 KB, e due livelli di prestazioni diversi, ovvero 500 letture al secondo + 100 scritture al secondo e 500 letture al secondo + 500 scritture al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-178">For example, here's a table that shows how many request units to provision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="85b5d-179">La coerenza dei dati è stata configurata come Sessione e i criteri di indicizzazione sono stati impostati su Nessuno.</span><span class="sxs-lookup"><span data-stu-id="85b5d-179">The data consistency was configured at Session, and the indexing policy was set to None.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="85b5d-180"><strong>Dimensioni dell'elemento</strong></span><span class="sxs-lookup"><span data-stu-id="85b5d-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-181"><strong>Letture al secondo</strong></span><span class="sxs-lookup"><span data-stu-id="85b5d-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-182"><strong>Scritture al secondo</strong></span><span class="sxs-lookup"><span data-stu-id="85b5d-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-183"><strong>Unità richiesta</strong></span><span class="sxs-lookup"><span data-stu-id="85b5d-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85b5d-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="85b5d-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-185">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-186">100</span><span class="sxs-lookup"><span data-stu-id="85b5d-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-187">(500 * 1) + (100 * 5) = 1.000 UR/sec</span><span class="sxs-lookup"><span data-stu-id="85b5d-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85b5d-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="85b5d-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-189">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-190">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-191">(500 * 1) + (500 * 5) = 3.000 UR/sec</span><span class="sxs-lookup"><span data-stu-id="85b5d-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85b5d-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="85b5d-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-193">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-194">100</span><span class="sxs-lookup"><span data-stu-id="85b5d-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-195">(500 * 1,3) + (100 * 7) = 1.350 UR/sec</span><span class="sxs-lookup"><span data-stu-id="85b5d-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85b5d-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="85b5d-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-197">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-198">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-199">(500 * 1,3) + (500 * 7) = 4.150 UR/sec</span><span class="sxs-lookup"><span data-stu-id="85b5d-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85b5d-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="85b5d-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-201">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-202">100</span><span class="sxs-lookup"><span data-stu-id="85b5d-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-203">(500 * 10) + (100 * 48) = 9.800 UR/sec</span><span class="sxs-lookup"><span data-stu-id="85b5d-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="85b5d-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="85b5d-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-205">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-206">500</span><span class="sxs-lookup"><span data-stu-id="85b5d-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="85b5d-207">(500 * 10) + (500 * 48) = 29.000 UR/sec</span><span class="sxs-lookup"><span data-stu-id="85b5d-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a><span data-ttu-id="85b5d-208">Usare il calcolatore di unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-208">Use the request unit calculator</span></span>
<span data-ttu-id="85b5d-209">Per semplificare l'ottimizzazione delle stime di velocità effettiva da parte dei clienti, è disponibile un [calcolatore di unità richiesta](https://www.documentdb.com/capacityplanner) , che consente di stimare i requisiti relativi alle unità richiesta per operazioni tipiche, incluse le seguenti:</span><span class="sxs-lookup"><span data-stu-id="85b5d-209">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="85b5d-210">Creazione di elementi (scrittura)</span><span class="sxs-lookup"><span data-stu-id="85b5d-210">Item creates (writes)</span></span>
* <span data-ttu-id="85b5d-211">Lettura di elementi</span><span class="sxs-lookup"><span data-stu-id="85b5d-211">Item reads</span></span>
* <span data-ttu-id="85b5d-212">Eliminazione di elementi</span><span class="sxs-lookup"><span data-stu-id="85b5d-212">Item deletes</span></span>
* <span data-ttu-id="85b5d-213">Aggiornamento di elementi</span><span class="sxs-lookup"><span data-stu-id="85b5d-213">Item updates</span></span>

<span data-ttu-id="85b5d-214">Lo strumento include anche il supporto per la stima delle esigenze di archiviazione dei dati in base agli elementi di esempio specificati.</span><span class="sxs-lookup"><span data-stu-id="85b5d-214">The tool also includes support for estimating data storage needs based on the sample items you provide.</span></span>

<span data-ttu-id="85b5d-215">L'uso dello strumento è molto semplice:</span><span class="sxs-lookup"><span data-stu-id="85b5d-215">Using the tool is simple:</span></span>

1. <span data-ttu-id="85b5d-216">Caricare uno o più elementi rappresentativi.</span><span class="sxs-lookup"><span data-stu-id="85b5d-216">Upload one or more representative items.</span></span>
   
    ![Caricare elementi nel calcolatore di unità richiesta][2]
2. <span data-ttu-id="85b5d-218">Per stimare i requisiti di archiviazione, immettere il numero totale di elementi che si prevede di archiviare.</span><span class="sxs-lookup"><span data-stu-id="85b5d-218">To estimate data storage requirements, enter the total number of items you expect to store.</span></span>
3. <span data-ttu-id="85b5d-219">Immettere il numero di operazioni di creazione, lettura, aggiornamento ed eliminazione degli elementi necessarie (al secondo).</span><span class="sxs-lookup"><span data-stu-id="85b5d-219">Enter the number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="85b5d-220">Per stimare gli addebiti delle unità richiesta per le operazioni di aggiornamento di elementi, caricare una copia dell'elemento di esempio usato nel passaggio 1 precedente che include aggiornamenti di campi tipici.</span><span class="sxs-lookup"><span data-stu-id="85b5d-220">To estimate the request unit charges of item update operations, upload a copy of the sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="85b5d-221">Ad esempio, se gli aggiornamenti di elementi modificano in genere due proprietà denominate lastLogin e userVisits, è sufficiente copiare l'elemento di esempio, aggiornare i valori per queste due proprietà e caricare l'elemento copiato.</span><span class="sxs-lookup"><span data-stu-id="85b5d-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy the sample item, update the values for those two properties, and upload the copied item.</span></span>
   
    ![Immettere i requisiti relativi alla velocità effettiva nel calcolatore di unità richiesta][3]
4. <span data-ttu-id="85b5d-223">Fare clic su Calcola ed esaminare i risultati.</span><span class="sxs-lookup"><span data-stu-id="85b5d-223">Click calculate and examine the results.</span></span>
   
    ![Risultati del calcolatore di unità richiesta][4]

> [!NOTE]
> <span data-ttu-id="85b5d-225">Se sono presenti tipi di elementi che variano notevolmente in termini di dimensioni e numero di proprietà indicizzate, caricare un campione di ogni *tipo* di elemento tipico nello strumento e quindi calcolare i risultati.</span><span class="sxs-lookup"><span data-stu-id="85b5d-225">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical item to the tool and then calculate the results.</span></span>
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="85b5d-226">Usare l'intestazione della risposta di addebito della richiesta di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85b5d-226">Use the Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="85b5d-227">Ogni risposta dal servizio Azure Cosmos DB include un'intestazione personalizzata (`x-ms-request-charge`) che contiene le unità richiesta utilizzate per la richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-227">Every response from the Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span></span> <span data-ttu-id="85b5d-228">Questa intestazione è accessibile anche tramite gli SDK di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85b5d-228">This header is also accessible through the Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="85b5d-229">In .NET SDK, RequestCharge è una proprietà dell'oggetto ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="85b5d-229">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span></span>  <span data-ttu-id="85b5d-230">Per quanto riguarda le query, Esplora query di Azure Cosmos DB nel portale di Azure fornisce informazioni sull'addebito per le richieste relative alle query eseguite.</span><span class="sxs-lookup"><span data-stu-id="85b5d-230">For queries, the Azure Cosmos DB Query Explorer in the Azure portal provides request charge information for executed queries.</span></span>

![Analisi degli addebiti delle unità richiesta in Esplora Query][1]

<span data-ttu-id="85b5d-232">Con questa premessa, un metodo per stimare la quantità di velocità effettiva riservata richiesta dall'applicazione consiste nel registrare l'addebito delle unità richiesta associato all'esecuzione di operazioni tipiche rispetto a un elemento rappresentativo usato dall'applicazione e quindi nello stimare il numero di operazioni che si prevede di eseguire al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-232">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="85b5d-233">Assicurarsi di misurare e includere anche le query tipiche e l'utilizzo di script di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="85b5d-233">Be sure to measure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="85b5d-234">Se sono presenti tipi di elementi che variano notevolmente in termini di dimensioni e numero di proprietà indicizzate, registrare l'addebito delle unità richiesta per le operazioni applicabili associato a ogni *tipo* di elemento tipico.</span><span class="sxs-lookup"><span data-stu-id="85b5d-234">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="85b5d-235">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="85b5d-235">For example:</span></span>

1. <span data-ttu-id="85b5d-236">Registrare l'addebito delle unità richiesta di creazione (inserimento) di un elemento tipico.</span><span class="sxs-lookup"><span data-stu-id="85b5d-236">Record the request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="85b5d-237">Registrare l'addebito delle unità richiesta di lettura di un elemento tipico.</span><span class="sxs-lookup"><span data-stu-id="85b5d-237">Record the request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="85b5d-238">Registrare l'addebito delle unità richiesta di aggiornamento di un elemento tipico.</span><span class="sxs-lookup"><span data-stu-id="85b5d-238">Record the request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="85b5d-239">Registrare l'addebito delle unità richiesta di query tipiche su elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="85b5d-239">Record the request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="85b5d-240">Registrare l'addebito delle unità richiesta di tutti gli script personalizzati (stored procedure, trigger, funzioni definite dall'utente) utilizzati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85b5d-240">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span></span>
6. <span data-ttu-id="85b5d-241">Calcolare le unità richiesta necessarie in base al numero stimato di operazioni che si prevede di eseguire al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-241">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span></span>

### <span data-ttu-id="85b5d-242"><a id="GetLastRequestStatistics"></a>Usare il comando dell'API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="85b5d-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="85b5d-243">L'API per MongoDB supporta un comando personalizzato, *getLastRequestStatistics*, per il recupero degli addebiti per le richieste per operazioni specificate.</span><span class="sxs-lookup"><span data-stu-id="85b5d-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span></span>

<span data-ttu-id="85b5d-244">Ad esempio, in Mongo Shell eseguire l'operazione di cui si vuole verificare l'addebito per le richieste.</span><span class="sxs-lookup"><span data-stu-id="85b5d-244">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="85b5d-245">Eseguire quindi il comando *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="85b5d-245">Next, execute the command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="85b5d-246">Con questa premessa, un metodo per stimare la quantità di velocità effettiva riservata richiesta dall'applicazione consiste nel registrare l'addebito delle unità richiesta associato all'esecuzione di operazioni tipiche rispetto a un elemento rappresentativo usato dall'applicazione e quindi nello stimare il numero di operazioni che si prevede di eseguire al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-246">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="85b5d-247">Se sono presenti tipi di elementi che variano notevolmente in termini di dimensioni e numero di proprietà indicizzate, registrare l'addebito delle unità richiesta per le operazioni applicabili associato a ogni *tipo* di elemento tipico.</span><span class="sxs-lookup"><span data-stu-id="85b5d-247">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="85b5d-248">Usare le metriche del portale dell'API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="85b5d-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="85b5d-249">Il modo più semplice per ottenere una stima valida degli addebiti per le unità richiesta per il database dell'API per MongoDB consiste nell'usare le metriche del [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85b5d-249">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="85b5d-250">I grafici *Numero di richieste* e *Richiedi addebito* consentono di ottenere una stima del numero di unità richiesta utilizzate da ogni operazione e dal numero di unità richiesta utilizzate una rispetto all'altra.</span><span class="sxs-lookup"><span data-stu-id="85b5d-250">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![Metriche del portale dell'API per MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="85b5d-252">Esempio di stima delle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-252">A request unit estimation example</span></span>
<span data-ttu-id="85b5d-253">Considerare il documento da ~1 KB seguente:</span><span class="sxs-lookup"><span data-stu-id="85b5d-253">Consider the following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="85b5d-254">I documenti sono minimizzati in Azure Cosmos DB, quindi le dimensioni del documento precedente calcolate dal sistema sono leggermente inferiori a 1 KB.</span><span class="sxs-lookup"><span data-stu-id="85b5d-254">Documents are minified in Azure Cosmos DB, so the system calculated size of the document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="85b5d-255">La tabella seguente mostra gli addebiti delle unità richiesta approssimativi per le operazioni tipiche su questo elemento. L'addebito delle unità richiesta approssimativo presuppone che il livello di coerenza dell'account sia impostato su "Sessione" e che tutti gli elementi siano indicizzati automaticamente:</span><span class="sxs-lookup"><span data-stu-id="85b5d-255">The following table shows approximate request unit charges for typical operations on this item (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="85b5d-256">Operazione</span><span class="sxs-lookup"><span data-stu-id="85b5d-256">Operation</span></span> | <span data-ttu-id="85b5d-257">Addebito delle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="85b5d-258">Creare elemento</span><span class="sxs-lookup"><span data-stu-id="85b5d-258">Create item</span></span> |<span data-ttu-id="85b5d-259">~15 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-259">~15 RU</span></span> |
| <span data-ttu-id="85b5d-260">Leggere l'elemento</span><span class="sxs-lookup"><span data-stu-id="85b5d-260">Read item</span></span> |<span data-ttu-id="85b5d-261">~1 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-261">~1 RU</span></span> |
| <span data-ttu-id="85b5d-262">Eseguire query sull'elemento in base all'ID</span><span class="sxs-lookup"><span data-stu-id="85b5d-262">Query item by id</span></span> |<span data-ttu-id="85b5d-263">~2,5 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-263">~2.5 RU</span></span> |

<span data-ttu-id="85b5d-264">Questa tabella mostra anche gli addebiti approssimativi delle unità richiesta per le query tipiche usate nell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="85b5d-264">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span></span>

| <span data-ttu-id="85b5d-265">Query</span><span class="sxs-lookup"><span data-stu-id="85b5d-265">Query</span></span> | <span data-ttu-id="85b5d-266">Addebito delle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-266">Request Unit Charge</span></span> | <span data-ttu-id="85b5d-267">Numero di elementi restituiti</span><span class="sxs-lookup"><span data-stu-id="85b5d-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85b5d-268">Selezionare alimenti in base all'ID</span><span class="sxs-lookup"><span data-stu-id="85b5d-268">Select food by id</span></span> |<span data-ttu-id="85b5d-269">~2,5 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-269">~2.5 RU</span></span> |<span data-ttu-id="85b5d-270">1</span><span class="sxs-lookup"><span data-stu-id="85b5d-270">1</span></span> |
| <span data-ttu-id="85b5d-271">Selezionare alimenti in base al produttore</span><span class="sxs-lookup"><span data-stu-id="85b5d-271">Select foods by manufacturer</span></span> |<span data-ttu-id="85b5d-272">~7 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-272">~7 RU</span></span> |<span data-ttu-id="85b5d-273">7</span><span class="sxs-lookup"><span data-stu-id="85b5d-273">7</span></span> |
| <span data-ttu-id="85b5d-274">Selezionare per gruppo di alimenti e ordinare in base al peso</span><span class="sxs-lookup"><span data-stu-id="85b5d-274">Select by food group and order by weight</span></span> |<span data-ttu-id="85b5d-275">~70 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-275">~70 RU</span></span> |<span data-ttu-id="85b5d-276">100</span><span class="sxs-lookup"><span data-stu-id="85b5d-276">100</span></span> |
| <span data-ttu-id="85b5d-277">Selezionare i primi 10 alimenti in un gruppo di alimenti</span><span class="sxs-lookup"><span data-stu-id="85b5d-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="85b5d-278">~10 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="85b5d-278">~10 RU</span></span> |<span data-ttu-id="85b5d-279">10</span><span class="sxs-lookup"><span data-stu-id="85b5d-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="85b5d-280">Gli addebiti delle unità richiesta variano in base al numero di elementi restituiti.</span><span class="sxs-lookup"><span data-stu-id="85b5d-280">RU charges vary based on the number of items returned.</span></span>
> 
> 

<span data-ttu-id="85b5d-281">Con queste informazioni è possibile stimare i requisiti relativi alle unità richiesta per questa applicazione, dato il numero di operazioni e le query previste al secondo:</span><span class="sxs-lookup"><span data-stu-id="85b5d-281">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="85b5d-282">Operazione/query</span><span class="sxs-lookup"><span data-stu-id="85b5d-282">Operation/Query</span></span> | <span data-ttu-id="85b5d-283">Numero stimato al secondo</span><span class="sxs-lookup"><span data-stu-id="85b5d-283">Estimated number per second</span></span> | <span data-ttu-id="85b5d-284">Unità richiesta necessarie</span><span class="sxs-lookup"><span data-stu-id="85b5d-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85b5d-285">Creare elemento</span><span class="sxs-lookup"><span data-stu-id="85b5d-285">Create item</span></span> |<span data-ttu-id="85b5d-286">10</span><span class="sxs-lookup"><span data-stu-id="85b5d-286">10</span></span> |<span data-ttu-id="85b5d-287">150</span><span class="sxs-lookup"><span data-stu-id="85b5d-287">150</span></span> |
| <span data-ttu-id="85b5d-288">Leggere l'elemento</span><span class="sxs-lookup"><span data-stu-id="85b5d-288">Read item</span></span> |<span data-ttu-id="85b5d-289">100</span><span class="sxs-lookup"><span data-stu-id="85b5d-289">100</span></span> |<span data-ttu-id="85b5d-290">100</span><span class="sxs-lookup"><span data-stu-id="85b5d-290">100</span></span> |
| <span data-ttu-id="85b5d-291">Selezionare alimenti in base al produttore</span><span class="sxs-lookup"><span data-stu-id="85b5d-291">Select foods by manufacturer</span></span> |<span data-ttu-id="85b5d-292">25</span><span class="sxs-lookup"><span data-stu-id="85b5d-292">25</span></span> |<span data-ttu-id="85b5d-293">175</span><span class="sxs-lookup"><span data-stu-id="85b5d-293">175</span></span> |
| <span data-ttu-id="85b5d-294">Selezionare per gruppo di alimenti</span><span class="sxs-lookup"><span data-stu-id="85b5d-294">Select by food group</span></span> |<span data-ttu-id="85b5d-295">10</span><span class="sxs-lookup"><span data-stu-id="85b5d-295">10</span></span> |<span data-ttu-id="85b5d-296">700</span><span class="sxs-lookup"><span data-stu-id="85b5d-296">700</span></span> |
| <span data-ttu-id="85b5d-297">Selezionare i primi 10</span><span class="sxs-lookup"><span data-stu-id="85b5d-297">Select top 10</span></span> |<span data-ttu-id="85b5d-298">15</span><span class="sxs-lookup"><span data-stu-id="85b5d-298">15</span></span> |<span data-ttu-id="85b5d-299">Totale 150</span><span class="sxs-lookup"><span data-stu-id="85b5d-299">150 Total</span></span> |

<span data-ttu-id="85b5d-300">In questo caso, è previsto un requisito di velocità effettiva medio di 1.275 unità richiesta/secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="85b5d-301">Arrotondando alle 100 più vicine, si dovrà effettuare il provisioning di 1.300 unità richiesta/secondo per la raccolta dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85b5d-301">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="85b5d-302"><a id="RequestRateTooLarge"></a> Superamento dei limiti della velocità effettiva riservata in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85b5d-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="85b5d-303">Tenere presente che, in assenza di budget, il consumo delle unità richiesta è valutato in base a una frequenza al secondo.</span><span class="sxs-lookup"><span data-stu-id="85b5d-303">Recall that request unit consumption is evaluated as a rate per second if the budget is empty.</span></span> <span data-ttu-id="85b5d-304">Per le applicazioni che superano il livello di unità richiesta di cui è stato effettuato il provisioning per un contenitore, le richieste saranno limitate fino al ritorno del livello sotto il valore riservato.</span><span class="sxs-lookup"><span data-stu-id="85b5d-304">For applications that exceed the provisioned request unit rate for a container, requests to that collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="85b5d-305">Nel caso di una limitazione, il server termina preventivamente la richiesta con RequestRateTooLargeException (codice di stato HTTP 429) e restituisce l'intestazione x-ms-retry-after-ms, che indica la quantità di tempo, in millisecondi, che l'utente deve attendere prima di eseguire di nuovo la richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-305">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="85b5d-306">Se si usano le query LINQ e .NET SDK per client, non è quasi mai necessario gestire questa eccezione, perché la versione corrente di .NET SDK per client rileva la risposta in modo implicito, rispetta l'intestazione retry-after specificata dal server e ripete la richiesta.</span><span class="sxs-lookup"><span data-stu-id="85b5d-306">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span></span> <span data-ttu-id="85b5d-307">A meno che all'account non accedano contemporaneamente più client, il tentativo successivo riuscirà.</span><span class="sxs-lookup"><span data-stu-id="85b5d-307">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span></span>

<span data-ttu-id="85b5d-308">Se più client operano collettivamente al di sopra della frequenza delle richieste, il comportamento di ripetizione dei tentativi predefinito potrebbe non essere sufficiente e il client genererà una DocumentClientException con codice di stato 429 per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85b5d-308">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span></span> <span data-ttu-id="85b5d-309">In casi come questo, si può valutare la possibilità di gestire la logica e il comportamento di ripetizione dei tentativi nelle routine di gestione degli errori dell'applicazione o di aumentare la velocità effettiva riservata per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="85b5d-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the container.</span></span>

## <span data-ttu-id="85b5d-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Superamento dei limiti della velocità effettiva riservata nell'API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="85b5d-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="85b5d-311">Le applicazioni che superano il livello di unità di richiesta con provisioning per una raccolta saranno limitate fino al ritorno del livello sotto il valore riservato.</span><span class="sxs-lookup"><span data-stu-id="85b5d-311">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="85b5d-312">In caso di limitazione, il back-end terminerà preventivamente la richiesta con un codice errore *16500*, ovvero *Troppe richieste*.</span><span class="sxs-lookup"><span data-stu-id="85b5d-312">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="85b5d-313">Per impostazione predefinita, l'API per MongoDB ripeterà automaticamente i tentativi fino a 10 volte prima di restituire un codice errore di tipo *Troppe richieste*.</span><span class="sxs-lookup"><span data-stu-id="85b5d-313">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="85b5d-314">Se si riceve un numero eccessivo di codici errore di tipo *Troppe richieste*, è possibile prendere in considerazione l'aggiunta del comportamento di ripetizione dei tentativi nelle routine di gestione degli errori dell'applicazione oppure l'[aumento della velocità effettiva riservata per la raccolta](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="85b5d-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85b5d-315">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85b5d-315">Next steps</span></span>
<span data-ttu-id="85b5d-316">Per altre informazioni sulla velocità effettiva riservata con i database Azure Cosmos DB, vedere queste risorse:</span><span class="sxs-lookup"><span data-stu-id="85b5d-316">To learn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="85b5d-317">Prezzi di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85b5d-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="85b5d-318">Partizionamento dei dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="85b5d-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="85b5d-319">Per altre informazioni su Azure Cosmos DB, vedere la relativa [documentazione](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="85b5d-319">To learn more about Azure Cosmos DB, see the Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="85b5d-320">Per iniziare a testare la scalabilità e le prestazioni con Azure Cosmos DB, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="85b5d-320">To get started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
