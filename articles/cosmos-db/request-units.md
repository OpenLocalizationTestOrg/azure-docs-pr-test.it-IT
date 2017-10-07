---
title: "aaaRequest unità di misura e stima della velocità effettiva - DB Cosmos Azure | Documenti Microsoft"
description: "Informazioni su come specificare toounderstand e stimare i requisiti dell'unità richiesta nel database di Azure Cosmos."
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
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="523d1-103">Unità richiesta in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="523d1-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="523d1-104">Ora disponibile: [calcolatore di unità richiesta](https://www.documentdb.com/capacityplanner) di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="523d1-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="523d1-105">Per altre informazioni, vedere [Stima delle esigenze di velocità effettiva](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="523d1-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Calcolatore della velocità effettiva][5]

## <a name="introduction"></a><span data-ttu-id="523d1-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="523d1-107">Introduction</span></span>
<span data-ttu-id="523d1-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) è il database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="523d1-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="523d1-109">Con Azure Cosmos DB, non dispone di macchine virtuali toorent, distribuire il software o monitorare i database.</span><span class="sxs-lookup"><span data-stu-id="523d1-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="523d1-110">Azure DB Cosmos è gestito e monitorato costantemente da Microsoft tecnici superiore toodeliver world classe disponibilità, prestazioni e protezione dei dati.</span><span class="sxs-lookup"><span data-stu-id="523d1-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="523d1-111">Permette di accedere ai dati usando le API preferite, perché supporta in modalità nativa [SQL di DocumentDB](documentdb-sql-query.md) (documenti), MongoDB (documenti), [Archiviazione tabelle di Azure](https://azure.microsoft.com/services/storage/tables/) (chiave-valore) e [Gremlin](https://tinkerpop.apache.org/gremlin.html) (grafi).</span><span class="sxs-lookup"><span data-stu-id="523d1-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="523d1-112">valuta Hello del database di Azure Cosmos è hello unità richiesta (RU).</span><span class="sxs-lookup"><span data-stu-id="523d1-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="523d1-113">Con unità riservate, non è necessaria capacità di lettura/scrittura tooreserve o eseguire il provisioning della CPU, memoria e IOPS.</span><span class="sxs-lookup"><span data-stu-id="523d1-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="523d1-114">DB Cosmos Azure supporta una serie di API con diverse operazioni che vanno da semplici operazioni di lettura e scrittura toocomplex query grafico.</span><span class="sxs-lookup"><span data-stu-id="523d1-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="523d1-115">Poiché non tutte le richieste sono uguali, viene loro assegnata una quantità normalizzata **unità richieste** in base all'ammontare hello della richiesta di calcolo necessarie tooserve hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="523d1-116">numero di unità di richiesta per un'operazione di Hello è deterministica ed è possibile monitorare il numero di hello di unità di richiesta utilizzati da qualsiasi operazione nel database di Azure Cosmos tramite un'intestazione di risposta.</span><span class="sxs-lookup"><span data-stu-id="523d1-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="523d1-117">tooprovide prestazioni prevedibili, è necessario tooreserve velocità effettiva in unità di 100 UR/sec.</span><span class="sxs-lookup"><span data-stu-id="523d1-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="523d1-118">Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="523d1-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="523d1-119">Cosa sono le unità richiesta e gli addebiti richiesta?</span><span class="sxs-lookup"><span data-stu-id="523d1-119">What are request units and request charges?</span></span>
* <span data-ttu-id="523d1-120">Come è possibile specificare la capacità delle unità richiesta per una raccolta?</span><span class="sxs-lookup"><span data-stu-id="523d1-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="523d1-121">Come si possono stimare le esigenze relative alle unità richiesta per l'applicazione?</span><span class="sxs-lookup"><span data-stu-id="523d1-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="523d1-122">Cosa accade se si supera la capacità delle unità richiesta per una raccolta?</span><span class="sxs-lookup"><span data-stu-id="523d1-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="523d1-123">Come Azure Cosmos DB è un database di più modello, è importante toonote che si farà riferimento tooa insieme o documento per un documento di API, un nodo o un grafico per un grafico di API e una tabella o entità per la tabella API.</span><span class="sxs-lookup"><span data-stu-id="523d1-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="523d1-124">Velocità effettiva di questo documento generalizzeremo toohello concetti/elemento contenitore.</span><span class="sxs-lookup"><span data-stu-id="523d1-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="523d1-125">Unità richiesta e addebiti richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-125">Request units and request charges</span></span>
<span data-ttu-id="523d1-126">DB Cosmos Azure offre prestazioni rapida e prevedibile da *riservare* toosatisfy risorse esigenze di velocità effettiva dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="523d1-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="523d1-127">Perché l'applicazione carica e modifica di modelli nel corso del tempo di accesso, Azure Cosmos DB consente tooeasily aumentare o diminuire hello dell'applicazione disponibili tooyour velocità effettiva riservati.</span><span class="sxs-lookup"><span data-stu-id="523d1-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="523d1-128">Con Azure Cosmos DB, la velocità effettiva riservata è specificata in termini di unità richiesta elaborate al secondo.</span><span class="sxs-lookup"><span data-stu-id="523d1-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="523d1-129">È possibile considerare di unità di richiesta come valuta di velocità effettiva, in base al quale si *riservare* garantito che una quantità di unità di richiesta applicazione tooyour disponibili in base al secondo.</span><span class="sxs-lookup"><span data-stu-id="523d1-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="523d1-130">Ogni operazione in Azure Cosmos DB, ovvero scrittura di un documento, esecuzione di una query, aggiornamento di un documento, utilizza CPU, memoria e operazioni di I/O al secondo.</span><span class="sxs-lookup"><span data-stu-id="523d1-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="523d1-131">In altre parole, ogni operazione comporta un *addebito richiesta* espresso in *unità richiesta*.</span><span class="sxs-lookup"><span data-stu-id="523d1-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="523d1-132">I fattori che influiscono sulle spese di unità di richiesta, insieme ai requisiti di velocità effettiva dell'applicazione, hello conoscendo toorun è l'applicazione come costi in modo efficace possibile.</span><span class="sxs-lookup"><span data-stu-id="523d1-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="523d1-133">Esplora query Hello è anche un'eccellente strumento tootest hello di base di una query.</span><span class="sxs-lookup"><span data-stu-id="523d1-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="523d1-134">Si consiglia di iniziare, è possibile guardare hello seguente video, in cui Aravind Ramachandran illustra l'unità di richiesta e prestazioni prevedibili con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="523d1-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="523d1-135">Specifica della capacità in unità richiesta in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="523d1-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="523d1-136">Quando si avvia una nuova raccolta, tabella o grafico, specificare il numero di hello di unità di richiesta al secondo (UR al secondo) si desidera riservato.</span><span class="sxs-lookup"><span data-stu-id="523d1-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="523d1-137">In base alla velocità effettiva di provisioning hello, Azure Cosmos DB alloca la raccolta di partizioni fisiche toohost e divisioni/rebalances dati tra partizioni di si sviluppa.</span><span class="sxs-lookup"><span data-stu-id="523d1-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="523d1-138">DB Cosmos Azure richiede che un toobe chiave di partizione specificato quando una raccolta è stato eseguito il provisioning con 2.500 unità di richiesta o una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="523d1-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="523d1-139">Una chiave di partizione è anche necessario tooscale la velocità effettiva della raccolta oltre 2.500 unità di richiesta in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="523d1-140">Pertanto, è consigliabile tooconfigure un [chiave di partizione](partition-data.md) quando si crea un contenitore indipendentemente dal fatto la velocità effettiva di iniziale.</span><span class="sxs-lookup"><span data-stu-id="523d1-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="523d1-141">Poiché i dati potrebbero contenere toobe suddiviso tra più partizioni, è necessario toopick una chiave di partizione che ha una cardinalità elevata (100 toomillions di valori distinct) in modo che la raccolta/tabella o grafico e le richieste possono essere ridimensionate in modo uniforme da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="523d1-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="523d1-142">Una chiave di partizione è un limite logico, non un limite fisico.</span><span class="sxs-lookup"><span data-stu-id="523d1-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="523d1-143">Pertanto, non è necessario numero hello toolimit partizione distinta dei valori di chiave.</span><span class="sxs-lookup"><span data-stu-id="523d1-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="523d1-144">In realtà è migliore toohave più distinta partizionare i valori di chiave inferiore rispetto a come Azure Cosmos DB con le opzioni di bilanciamento del carico di ulteriori.</span><span class="sxs-lookup"><span data-stu-id="523d1-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="523d1-145">Ecco un frammento di codice per la creazione di una raccolta con 3.000 richiesta unità al secondo utilizzando hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="523d1-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="523d1-146">Azure Cosmos DB usa un modello di prenotazione per la velocità effettiva,</span><span class="sxs-lookup"><span data-stu-id="523d1-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="523d1-147">Ovvero, vengono fatturati quantità hello di velocità effettiva *riservato*, indipendentemente da quanta parte di tale velocità effettiva è attivamente *utilizzato*.</span><span class="sxs-lookup"><span data-stu-id="523d1-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="523d1-148">Come carico, dati e utilizzo dei modelli modifica dell'applicazione è possibile ridimensionare su e giù hello quantità di RUs riservato tramite SDK o l'utilizzo di hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="523d1-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="523d1-149">Viene eseguito il mapping di ogni raccolta, tabella o grafico tooan `Offer` risorse in Azure Cosmos DB, che contiene i metadati relativi a velocità effettiva di provisioning hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="523d1-150">È possibile modificare la velocità effettiva hello allocato, la ricerca di risorsa offerta corrispondente hello per un contenitore, quindi aggiornarla con il nuovo valore di velocità effettiva hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="523d1-151">Ecco un frammento di codice per la modifica di velocità effettiva di hello di una raccolta di too5, 000 unità di richiesta al secondo utilizzando hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="523d1-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="523d1-152">Quando si modifica la velocità effettiva hello non è disponibilità toohello impatto del contenitore.</span><span class="sxs-lookup"><span data-stu-id="523d1-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="523d1-153">Velocità effettiva riservate hello è in genere efficace entro pochi secondi sull'applicazione di velocità effettiva di nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="523d1-154">Considerazioni sulle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-154">Request unit considerations</span></span>
<span data-ttu-id="523d1-155">Quando si stima il numero di hello di tooreserve unità di richiesta per il contenitore di Azure Cosmos DB, è importante tootake hello seguenti variabili in considerazione:</span><span class="sxs-lookup"><span data-stu-id="523d1-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="523d1-156">**Dimensioni dell'elemento**.</span><span class="sxs-lookup"><span data-stu-id="523d1-156">**Item size**.</span></span> <span data-ttu-id="523d1-157">Come dimensioni aumentano hello unità utilizzate tooread o scrittura dei dati hello comporterà un aumento.</span><span class="sxs-lookup"><span data-stu-id="523d1-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="523d1-158">**Numero di proprietà dell'elemento**.</span><span class="sxs-lookup"><span data-stu-id="523d1-158">**Item property count**.</span></span> <span data-ttu-id="523d1-159">Presupponendo che l'impostazione predefinita l'indicizzazione di tutte le proprietà, hello unità utilizzate toowrite un documento, nodo/ntity aumenterà man mano che aumenta di hello proprietà count.</span><span class="sxs-lookup"><span data-stu-id="523d1-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="523d1-160">**Coerenza dei dati**.</span><span class="sxs-lookup"><span data-stu-id="523d1-160">**Data consistency**.</span></span> <span data-ttu-id="523d1-161">Quando si utilizzano livelli di coerenza dei dati di sicuro o con obsolescenza associata, unità aggiuntive saranno elementi tooread utilizzato.</span><span class="sxs-lookup"><span data-stu-id="523d1-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="523d1-162">**Proprietà indicizzate**.</span><span class="sxs-lookup"><span data-stu-id="523d1-162">**Indexed properties**.</span></span> <span data-ttu-id="523d1-163">I criteri di indicizzazione in ogni contenitore determinano le proprietà che vengono indicizzate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="523d1-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="523d1-164">È possibile ridurre il consumo di unità di richiesta, limitando il numero di hello di proprietà indicizzate o abilitare questo tipo di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="523d1-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="523d1-165">**Indicizzazione del documento**.</span><span class="sxs-lookup"><span data-stu-id="523d1-165">**Document indexing**.</span></span> <span data-ttu-id="523d1-166">Per impostazione predefinita, che ogni elemento viene automaticamente indicizzato, si utilizzerà un minor numero di unità di richiesta se si sceglie non tooindex alcuni degli elementi.</span><span class="sxs-lookup"><span data-stu-id="523d1-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="523d1-167">**Modelli di query**.</span><span class="sxs-lookup"><span data-stu-id="523d1-167">**Query patterns**.</span></span> <span data-ttu-id="523d1-168">complessità Hello di una query ha un impatto quante unità di richiesta vengono utilizzate per un'operazione.</span><span class="sxs-lookup"><span data-stu-id="523d1-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="523d1-169">numero di Hello di predicati, natura dei predicati hello, proiezioni, numero di funzioni definite dall'utente e dimensioni di hello del set di dati di origine hello tutti influenzare il costo di hello di operazioni di query.</span><span class="sxs-lookup"><span data-stu-id="523d1-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="523d1-170">**Utilizzo di script**.</span><span class="sxs-lookup"><span data-stu-id="523d1-170">**Script usage**.</span></span>  <span data-ttu-id="523d1-171">Come con le query, stored procedure e trigger utilizzano unità di richiesta in base hello complessità delle operazioni di hello in corso.</span><span class="sxs-lookup"><span data-stu-id="523d1-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="523d1-172">Quando si sviluppa l'applicazione, controllare i costi richiesta hello toobetter intestazione comprendere come ogni operazione sta consumando capacità dell'unità richiesta.</span><span class="sxs-lookup"><span data-stu-id="523d1-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="523d1-173">Stima delle esigenze di velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="523d1-173">Estimating throughput needs</span></span>
<span data-ttu-id="523d1-174">Un'unità di richiesta è una misura normalizzata del costo di elaborazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="523d1-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="523d1-175">Un'unità singola richiesta rappresenta tooread di capacità necessaria elaborazione hello (tramite collegamento self link o id) di un singolo 1KB elemento costituito da 10 valori di proprietà univoco (escluse le proprietà di sistema).</span><span class="sxs-lookup"><span data-stu-id="523d1-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="523d1-176">Un toocreate richiesta (insert), sostituire o eliminare hello stesso elemento utilizzerà ulteriore elaborazione dal servizio hello e in tal modo unità più richieste.</span><span class="sxs-lookup"><span data-stu-id="523d1-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="523d1-177">linea di base di Hello dell'unità di 1 richiesta di un 1KB corrisponde elemento tooa semplice ottenere collegamento self link o id dell'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="523d1-178">Ad esempio, ecco una tabella che mostra il numero di richieste tooprovision unità a tre dimensioni di elemento diverso (64KB, 1KB e 4KB) e a due diversi livelli di prestazioni (500 letture al secondo 100 scritture al secondo e 500 letture al secondo + 500 scritture al secondo).</span><span class="sxs-lookup"><span data-stu-id="523d1-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="523d1-179">è stata configurata la coerenza dei dati Hello nella sessione e criteri di indicizzazione hello è stato impostato tooNone.</span><span class="sxs-lookup"><span data-stu-id="523d1-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="523d1-180"><strong>Dimensioni dell'elemento</strong></span><span class="sxs-lookup"><span data-stu-id="523d1-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-181"><strong>Letture al secondo</strong></span><span class="sxs-lookup"><span data-stu-id="523d1-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-182"><strong>Scritture al secondo</strong></span><span class="sxs-lookup"><span data-stu-id="523d1-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-183"><strong>Unità richiesta</strong></span><span class="sxs-lookup"><span data-stu-id="523d1-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="523d1-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="523d1-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-185">500</span><span class="sxs-lookup"><span data-stu-id="523d1-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-186">100</span><span class="sxs-lookup"><span data-stu-id="523d1-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-187">(500 * 1) + (100 * 5) = 1.000 UR/sec</span><span class="sxs-lookup"><span data-stu-id="523d1-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="523d1-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="523d1-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-189">500</span><span class="sxs-lookup"><span data-stu-id="523d1-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-190">500</span><span class="sxs-lookup"><span data-stu-id="523d1-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-191">(500 * 1) + (500 * 5) = 3.000 UR/sec</span><span class="sxs-lookup"><span data-stu-id="523d1-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="523d1-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="523d1-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-193">500</span><span class="sxs-lookup"><span data-stu-id="523d1-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-194">100</span><span class="sxs-lookup"><span data-stu-id="523d1-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-195">(500 * 1,3) + (100 * 7) = 1.350 UR/sec</span><span class="sxs-lookup"><span data-stu-id="523d1-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="523d1-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="523d1-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-197">500</span><span class="sxs-lookup"><span data-stu-id="523d1-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-198">500</span><span class="sxs-lookup"><span data-stu-id="523d1-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-199">(500 * 1,3) + (500 * 7) = 4.150 UR/sec</span><span class="sxs-lookup"><span data-stu-id="523d1-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="523d1-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="523d1-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-201">500</span><span class="sxs-lookup"><span data-stu-id="523d1-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-202">100</span><span class="sxs-lookup"><span data-stu-id="523d1-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-203">(500 * 10) + (100 * 48) = 9.800 UR/sec</span><span class="sxs-lookup"><span data-stu-id="523d1-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="523d1-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="523d1-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-205">500</span><span class="sxs-lookup"><span data-stu-id="523d1-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-206">500</span><span class="sxs-lookup"><span data-stu-id="523d1-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="523d1-207">(500 * 10) + (500 * 48) = 29.000 UR/sec</span><span class="sxs-lookup"><span data-stu-id="523d1-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="523d1-208">Calcolatore unità richiesta hello</span><span class="sxs-lookup"><span data-stu-id="523d1-208">Use hello request unit calculator</span></span>
<span data-ttu-id="523d1-209">i clienti toohelp fini di ottimizzare le stime di velocità effettiva, non vi è un sito web basato [calcolatrice unità richiesta](https://www.documentdb.com/capacityplanner) toohelp stima hello richiesta i requisiti dell'unità per le normali operazioni, tra cui:</span><span class="sxs-lookup"><span data-stu-id="523d1-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="523d1-210">Creazione di elementi (scrittura)</span><span class="sxs-lookup"><span data-stu-id="523d1-210">Item creates (writes)</span></span>
* <span data-ttu-id="523d1-211">Lettura di elementi</span><span class="sxs-lookup"><span data-stu-id="523d1-211">Item reads</span></span>
* <span data-ttu-id="523d1-212">Eliminazione di elementi</span><span class="sxs-lookup"><span data-stu-id="523d1-212">Item deletes</span></span>
* <span data-ttu-id="523d1-213">Aggiornamento di elementi</span><span class="sxs-lookup"><span data-stu-id="523d1-213">Item updates</span></span>

<span data-ttu-id="523d1-214">strumento Hello include inoltre il supporto per la stima delle esigenze di archiviazione dei dati in base agli elementi di esempio hello che è fornire.</span><span class="sxs-lookup"><span data-stu-id="523d1-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="523d1-215">Utilizzo dello strumento di hello è semplice:</span><span class="sxs-lookup"><span data-stu-id="523d1-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="523d1-216">Caricare uno o più elementi rappresentativi.</span><span class="sxs-lookup"><span data-stu-id="523d1-216">Upload one or more representative items.</span></span>
   
    ![Caricare calcolatrice unità richiesta toohello di elementi][2]
2. <span data-ttu-id="523d1-218">requisiti di archiviazione dati tooestimate, immettere il numero totale di hello degli elementi previsti toostore.</span><span class="sxs-lookup"><span data-stu-id="523d1-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="523d1-219">Immettere numero hello di elementi di creare, leggere, aggiornare ed eliminare le operazioni desiderate (in base al secondo).</span><span class="sxs-lookup"><span data-stu-id="523d1-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="523d1-220">gli addebiti unità di richiesta di tooestimate hello elemento operazioni di aggiornamento, caricare una copia dell'elemento di esempio hello dal passaggio 1 sopra che include aggiornamenti del campo tipico.</span><span class="sxs-lookup"><span data-stu-id="523d1-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="523d1-221">Ad esempio, se gli aggiornamenti degli elementi in genere modificare due proprietà denominate lastLogin e userVisits, copiare semplicemente l'elemento di esempio hello, aggiornare i valori hello per queste due proprietà e carica elemento hello copiato.</span><span class="sxs-lookup"><span data-stu-id="523d1-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Immettere i requisiti di velocità effettiva della calcolatrice unità di richiesta hello][3]
4. <span data-ttu-id="523d1-223">Fare clic su calcolare ed esaminare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-223">Click calculate and examine hello results.</span></span>
   
    ![Risultati del calcolatore di unità richiesta][4]

> [!NOTE]
> <span data-ttu-id="523d1-225">Se si dispone di tipi di elemento che variano notevolmente in termini di dimensioni e hello il numero di proprietà indicizzate, quindi caricare un esempio di ogni *tipo* di toohello tipico elemento strumento e quindi calcolare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="523d1-226">Utilizzare l'intestazione della risposta addebito hello Azure Cosmos DB richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="523d1-227">Ogni risposta dal servizio Azure Cosmos DB hello include un'intestazione personalizzata (`x-ms-request-charge`) che contiene l'unità di richiesta hello utilizzata per la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="523d1-228">Questa intestazione è anche possibile accedere tramite hello Azure Cosmos DB SDK.</span><span class="sxs-lookup"><span data-stu-id="523d1-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="523d1-229">In .NET SDK hello, RequestCharge è una proprietà dell'oggetto ResourceResponse hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="523d1-230">Per le query, hello Azure Cosmos DB Query Esplora in hello portale di Azure fornisce informazioni di addebito richiesta per le query eseguite.</span><span class="sxs-lookup"><span data-stu-id="523d1-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![Esaminare gli addebiti RU in hello Esplora Query][1]

<span data-ttu-id="523d1-232">A tal fine, un metodo per la stima delle quantità hello di velocità effettiva riservati richiesta dall'applicazione è l'addebito di toorecord hello richiesta unità associata a eseguire le operazioni tipiche di un elemento rappresentativo utilizzato dall'applicazione e quindi stima hello numero di operazioni prevede l'esecuzione di ogni secondo.</span><span class="sxs-lookup"><span data-stu-id="523d1-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="523d1-233">Toomeasure assicurarsi di essere e includono query tipiche e uso degli script di Azure Cosmos DB anche.</span><span class="sxs-lookup"><span data-stu-id="523d1-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="523d1-234">Se si dispone di tipi di elemento che variano notevolmente in termini di dimensioni e hello il numero di proprietà indicizzate, quindi registrare addebito di hello operazione applicabile richiesta unità associata a ogni *tipo* dell'elemento tipico.</span><span class="sxs-lookup"><span data-stu-id="523d1-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="523d1-235">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="523d1-235">For example:</span></span>

1. <span data-ttu-id="523d1-236">Registrare l'addebito di unità hello richiesta di creazione (inserimento) un tipico elemento.</span><span class="sxs-lookup"><span data-stu-id="523d1-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="523d1-237">Addebito di unità hello record richiesta di lettura di un tipico elemento.</span><span class="sxs-lookup"><span data-stu-id="523d1-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="523d1-238">Addebito di unità hello record richiesta di aggiornamento di un tipico elemento.</span><span class="sxs-lookup"><span data-stu-id="523d1-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="523d1-239">Addebito di unità hello record richiesta di query comuni, tipico elemento.</span><span class="sxs-lookup"><span data-stu-id="523d1-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="523d1-240">Record hello richiesta unità delle spese di tutti gli script personalizzati (stored procedure, trigger, funzioni definite dall'utente) utilizzata da un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="523d1-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="523d1-241">Calcolare richiesta necessarie di hello unità hello stimato un numero di operazioni che si prevede toorun ogni secondo.</span><span class="sxs-lookup"><span data-stu-id="523d1-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="523d1-242"><a id="GetLastRequestStatistics"></a>Usare il comando dell'API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="523d1-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="523d1-243">API per MongoDB supporta un comando personalizzato, *getLastRequestStatistics*, per il recupero dei costi richiesta hello per le operazioni specificate.</span><span class="sxs-lookup"><span data-stu-id="523d1-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="523d1-244">Ad esempio, nella Shell di Mongo hello, eseguire hello operazione tooverify hello richiesta gratuito.</span><span class="sxs-lookup"><span data-stu-id="523d1-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="523d1-245">Successivamente, eseguire il comando hello *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="523d1-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
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

<span data-ttu-id="523d1-246">A tal fine, un metodo per la stima delle quantità hello di velocità effettiva riservati richiesta dall'applicazione è l'addebito di toorecord hello richiesta unità associata a eseguire le operazioni tipiche di un elemento rappresentativo utilizzato dall'applicazione e quindi stima hello numero di operazioni prevede l'esecuzione di ogni secondo.</span><span class="sxs-lookup"><span data-stu-id="523d1-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="523d1-247">Se si dispone di tipi di elemento che variano notevolmente in termini di dimensioni e hello il numero di proprietà indicizzate, quindi registrare addebito di hello operazione applicabile richiesta unità associata a ogni *tipo* dell'elemento tipico.</span><span class="sxs-lookup"><span data-stu-id="523d1-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="523d1-248">Usare le metriche del portale dell'API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="523d1-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="523d1-249">Hello più semplice tooget modo una buona stima dell'unità richiesta gli addebiti per l'API per i database di MongoDB è hello toouse [portale di Azure](https://portal.azure.com) metriche.</span><span class="sxs-lookup"><span data-stu-id="523d1-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="523d1-250">Con hello *numero di richieste* e *richiesta addebito* grafici, è possibile ottenere una stima il numero di unità di richiesta ogni operazione è il numero di unità di richiesta e un notevole utilizzano relativo tooone un altro.</span><span class="sxs-lookup"><span data-stu-id="523d1-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![Metriche del portale dell'API per MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="523d1-252">Esempio di stima delle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-252">A request unit estimation example</span></span>
<span data-ttu-id="523d1-253">Prendere in considerazione hello ~ 1KB documento seguenti:</span><span class="sxs-lookup"><span data-stu-id="523d1-253">Consider hello following ~1KB document:</span></span>

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
> <span data-ttu-id="523d1-254">I documenti sono minimizzare in Azure Cosmos DB, in modo che il sistema hello calcolato dimensioni del documento hello sopra sono leggermente inferiore a 1KB.</span><span class="sxs-lookup"><span data-stu-id="523d1-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="523d1-255">Hello nella tabella seguente mostra approssimativo richiesta gli addebiti di unità per le operazioni tipiche di questo elemento (hello richiesta approssimativo unità addebito si presuppone che a livello di coerenza hello account sia stato impostato troppo "Sessione" e che tutti gli elementi vengono indicizzati automaticamente):</span><span class="sxs-lookup"><span data-stu-id="523d1-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="523d1-256">Operazione</span><span class="sxs-lookup"><span data-stu-id="523d1-256">Operation</span></span> | <span data-ttu-id="523d1-257">Addebito delle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="523d1-258">Creare elemento</span><span class="sxs-lookup"><span data-stu-id="523d1-258">Create item</span></span> |<span data-ttu-id="523d1-259">~15 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-259">~15 RU</span></span> |
| <span data-ttu-id="523d1-260">Leggere l'elemento</span><span class="sxs-lookup"><span data-stu-id="523d1-260">Read item</span></span> |<span data-ttu-id="523d1-261">~1 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-261">~1 RU</span></span> |
| <span data-ttu-id="523d1-262">Eseguire query sull'elemento in base all'ID</span><span class="sxs-lookup"><span data-stu-id="523d1-262">Query item by id</span></span> |<span data-ttu-id="523d1-263">~2,5 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-263">~2.5 RU</span></span> |

<span data-ttu-id="523d1-264">Inoltre, gli addebiti di unità per le query tipiche utilizzato in un'applicazione hello questa tabella mostra approssimativo richiesta:</span><span class="sxs-lookup"><span data-stu-id="523d1-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="523d1-265">Query</span><span class="sxs-lookup"><span data-stu-id="523d1-265">Query</span></span> | <span data-ttu-id="523d1-266">Addebito delle unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-266">Request Unit Charge</span></span> | <span data-ttu-id="523d1-267">Numero di elementi restituiti</span><span class="sxs-lookup"><span data-stu-id="523d1-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="523d1-268">Selezionare alimenti in base all'ID</span><span class="sxs-lookup"><span data-stu-id="523d1-268">Select food by id</span></span> |<span data-ttu-id="523d1-269">~2,5 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-269">~2.5 RU</span></span> |<span data-ttu-id="523d1-270">1</span><span class="sxs-lookup"><span data-stu-id="523d1-270">1</span></span> |
| <span data-ttu-id="523d1-271">Selezionare alimenti in base al produttore</span><span class="sxs-lookup"><span data-stu-id="523d1-271">Select foods by manufacturer</span></span> |<span data-ttu-id="523d1-272">~7 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-272">~7 RU</span></span> |<span data-ttu-id="523d1-273">7</span><span class="sxs-lookup"><span data-stu-id="523d1-273">7</span></span> |
| <span data-ttu-id="523d1-274">Selezionare per gruppo di alimenti e ordinare in base al peso</span><span class="sxs-lookup"><span data-stu-id="523d1-274">Select by food group and order by weight</span></span> |<span data-ttu-id="523d1-275">~70 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-275">~70 RU</span></span> |<span data-ttu-id="523d1-276">100</span><span class="sxs-lookup"><span data-stu-id="523d1-276">100</span></span> |
| <span data-ttu-id="523d1-277">Selezionare i primi 10 alimenti in un gruppo di alimenti</span><span class="sxs-lookup"><span data-stu-id="523d1-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="523d1-278">~10 unità richiesta</span><span class="sxs-lookup"><span data-stu-id="523d1-278">~10 RU</span></span> |<span data-ttu-id="523d1-279">10</span><span class="sxs-lookup"><span data-stu-id="523d1-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="523d1-280">Gli addebiti RU variano in base numero hello di elementi restituiti.</span><span class="sxs-lookup"><span data-stu-id="523d1-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="523d1-281">Con queste informazioni, è possibile stimare i requisiti di RU hello per questo numero di hello applicazione data di operazioni e le query che si prevede che al secondo:</span><span class="sxs-lookup"><span data-stu-id="523d1-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="523d1-282">Operazione/query</span><span class="sxs-lookup"><span data-stu-id="523d1-282">Operation/Query</span></span> | <span data-ttu-id="523d1-283">Numero stimato al secondo</span><span class="sxs-lookup"><span data-stu-id="523d1-283">Estimated number per second</span></span> | <span data-ttu-id="523d1-284">Unità richiesta necessarie</span><span class="sxs-lookup"><span data-stu-id="523d1-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="523d1-285">Creare elemento</span><span class="sxs-lookup"><span data-stu-id="523d1-285">Create item</span></span> |<span data-ttu-id="523d1-286">10</span><span class="sxs-lookup"><span data-stu-id="523d1-286">10</span></span> |<span data-ttu-id="523d1-287">150</span><span class="sxs-lookup"><span data-stu-id="523d1-287">150</span></span> |
| <span data-ttu-id="523d1-288">Leggere l'elemento</span><span class="sxs-lookup"><span data-stu-id="523d1-288">Read item</span></span> |<span data-ttu-id="523d1-289">100</span><span class="sxs-lookup"><span data-stu-id="523d1-289">100</span></span> |<span data-ttu-id="523d1-290">100</span><span class="sxs-lookup"><span data-stu-id="523d1-290">100</span></span> |
| <span data-ttu-id="523d1-291">Selezionare alimenti in base al produttore</span><span class="sxs-lookup"><span data-stu-id="523d1-291">Select foods by manufacturer</span></span> |<span data-ttu-id="523d1-292">25</span><span class="sxs-lookup"><span data-stu-id="523d1-292">25</span></span> |<span data-ttu-id="523d1-293">175</span><span class="sxs-lookup"><span data-stu-id="523d1-293">175</span></span> |
| <span data-ttu-id="523d1-294">Selezionare per gruppo di alimenti</span><span class="sxs-lookup"><span data-stu-id="523d1-294">Select by food group</span></span> |<span data-ttu-id="523d1-295">10</span><span class="sxs-lookup"><span data-stu-id="523d1-295">10</span></span> |<span data-ttu-id="523d1-296">700</span><span class="sxs-lookup"><span data-stu-id="523d1-296">700</span></span> |
| <span data-ttu-id="523d1-297">Selezionare i primi 10</span><span class="sxs-lookup"><span data-stu-id="523d1-297">Select top 10</span></span> |<span data-ttu-id="523d1-298">15</span><span class="sxs-lookup"><span data-stu-id="523d1-298">15</span></span> |<span data-ttu-id="523d1-299">Totale 150</span><span class="sxs-lookup"><span data-stu-id="523d1-299">150 Total</span></span> |

<span data-ttu-id="523d1-300">In questo caso, è previsto un requisito di velocità effettiva medio di 1.275 unità richiesta/secondo.</span><span class="sxs-lookup"><span data-stu-id="523d1-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="523d1-301">Arrotondamento per eccesso toohello più vicino al 100, è necessario eseguire il provisioning 1.300 UR/sec per la raccolta di questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="523d1-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="523d1-302"><a id="RequestRateTooLarge"></a> Superamento dei limiti della velocità effettiva riservata in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="523d1-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="523d1-303">Tenere presente che il consumo di unità di richiesta viene valutato come una velocità al secondo se budget hello è vuoto.</span><span class="sxs-lookup"><span data-stu-id="523d1-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="523d1-304">Per le applicazioni che superano hello richiesta provisioning unità per un contenitore, richieste verrà limitata toothat raccolta fino a quando il tasso di hello scende di sotto di livello hello riservato.</span><span class="sxs-lookup"><span data-stu-id="523d1-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="523d1-305">Quando si verifica una limitazione, server hello modalità preemptive terminerà richiesta hello con RequestRateTooLargeException (codice di stato HTTP 429) e indicando l'intestazione x-ms-nuovo tentativo-dopo-ms hello restituito hello tempo totale, espresso in millisecondi, che hello utente deve attendere prima di Ritentare la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="523d1-306">Se si utilizza le query LINQ e .NET Client SDK di hello, quindi la maggior parte del tempo di hello non è mai necessario toodeal con questa eccezione, come versione corrente di hello del Client .NET SDK hello memorizza nella cache in modo implicito la risposta, equivalenti hello specificata dal server intestazione retry-after, e richiesta di hello tentativi.</span><span class="sxs-lookup"><span data-stu-id="523d1-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="523d1-307">A meno che non si accede all'account contemporaneamente da più client, il successivo tentativo di hello avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="523d1-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="523d1-308">Se si dispone di più di un client in modo cumulativo operativo sopra il numero di richieste di hello, hello comportamento tentativi predefinito potrebbe non essere sufficiente e client hello genererà un DocumentClientException con applicazione toohello 429 in codice stato.</span><span class="sxs-lookup"><span data-stu-id="523d1-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="523d1-309">In casi come questo, è possibile considerare la gestione di comportamento del nuovo tentativo e logica di errore dell'applicazione, la gestione di routine o aumentando la velocità effettiva riservati hello per contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="523d1-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="523d1-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Superamento dei limiti della velocità effettiva riservata nell'API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="523d1-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="523d1-311">Le applicazioni che superano l'unità di richiesta hello il provisioning per una raccolta verranno limitate fino a quando il tasso di hello scende di sotto di livello hello riservato.</span><span class="sxs-lookup"><span data-stu-id="523d1-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="523d1-312">Quando si verifica una limitazione, back-end hello terminerà modalità preemptive richiesta hello con un *16500* codice di errore - *troppo numerose richieste*.</span><span class="sxs-lookup"><span data-stu-id="523d1-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="523d1-313">Per impostazione predefinita, l'API per MongoDB tenterà automaticamente di ripetere too10 ore prima della restituzione di un *troppo numerose richieste* codice di errore.</span><span class="sxs-lookup"><span data-stu-id="523d1-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="523d1-314">Se si ricevono numerosi *troppo numerose richieste* codici di errore, è possibile considerare un comportamento del nuovo tentativo aggiunta nella routine di gestione degli errori dell'applicazione o [aumentando la velocità effettiva riservati hello per raccolta hello](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="523d1-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="523d1-315">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="523d1-315">Next steps</span></span>
<span data-ttu-id="523d1-316">toolearn ulteriori informazioni sulla velocità effettiva riservati con i database di Azure Cosmos DB, è esplorare queste risorse:</span><span class="sxs-lookup"><span data-stu-id="523d1-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="523d1-317">Prezzi di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="523d1-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="523d1-318">Partizionamento dei dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="523d1-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="523d1-319">toolearn ulteriori informazioni su Azure Cosmos DB, vedere hello Azure Cosmos DB [documentazione](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="523d1-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="523d1-320">tooget avviato con scala e test delle prestazioni con Azure Cosmos DB, vedere [test delle prestazioni e scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="523d1-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
