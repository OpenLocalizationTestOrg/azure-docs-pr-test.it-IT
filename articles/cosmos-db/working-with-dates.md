---
title: aaaWorking con date nel database di Azure Cosmos | Documenti Microsoft
description: Informazioni su come toowork con le date nel database di Azure Cosmos.
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="64b18-103">Uso delle date in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="64b18-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="64b18-104">Azure Cosmos DB offre flessibilità dello schema e un'indicizzazione avanzata tramite un modello di dati [JSON](http://www.json.org) nativo.</span><span class="sxs-lookup"><span data-stu-id="64b18-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="64b18-105">Tutte le risorse di Azure Cosmos DB, inclusi database, raccolte, documenti e procedure archiviate, sono modellate e archiviate come documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="64b18-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="64b18-106">Come requisito per essere portatile, JSON, insieme a Azure Cosmos DB, supporta solo un piccolo set di tipi di base: String, Number, Boolean, Array, Object e Null.</span><span class="sxs-lookup"><span data-stu-id="64b18-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="64b18-107">Tuttavia, JSON è flessibile e consente agli sviluppatori e Framework toorepresent tipi più complessi utilizzando queste primitive e componendoli come oggetti o matrici.</span><span class="sxs-lookup"><span data-stu-id="64b18-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="64b18-108">In tipi di base toohello inoltre, molte applicazioni necessario hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) digitare le date toorepresent e timestamp.</span><span class="sxs-lookup"><span data-stu-id="64b18-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="64b18-109">In questo articolo viene descritto come gli sviluppatori possono archiviare, recuperare e date nel database di Azure Cosmos utilizzando hello SDK .NET di query.</span><span class="sxs-lookup"><span data-stu-id="64b18-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="64b18-110">Archiviazione di valori DateTime</span><span class="sxs-lookup"><span data-stu-id="64b18-110">Storing DateTimes</span></span>
<span data-ttu-id="64b18-111">Per impostazione predefinita, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializza i valori DateTime come [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) stringhe.</span><span class="sxs-lookup"><span data-stu-id="64b18-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="64b18-112">La maggior parte delle applicazioni è possono utilizzare rappresentazione di stringa hello predefinito per DateTime per hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="64b18-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="64b18-113">Per confrontare stringhe e hello relativo ordinamento dei valori DateTime hello verrà mantenuto quando sono toostrings trasformato.</span><span class="sxs-lookup"><span data-stu-id="64b18-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="64b18-114">Questo approccio non richiede codici o attributi personalizzati per la conversione JSON.</span><span class="sxs-lookup"><span data-stu-id="64b18-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="64b18-115">le date di Hello archiviata in JSON sono risorse umane leggibile.</span><span class="sxs-lookup"><span data-stu-id="64b18-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="64b18-116">Questo approccio può sfruttare l'indicizzazione di Azure Cosmos DB per query più veloci.</span><span class="sxs-lookup"><span data-stu-id="64b18-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="64b18-117">Ad esempio, hello seguenti archivi di frammento di codice un `Order` oggetto che contiene due proprietà DateTime - `ShipDate` e `OrderDate` come un documento utilizzando hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="64b18-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="64b18-118">Il documento viene archiviato in Azure Cosmos DB come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="64b18-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="64b18-119">In alternativa, è possibile archiviare valori DateTime come timestamp Unix, vale a dire, come un numero che rappresenta il numero di hello di secondi trascorsi dal 1 gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="64b18-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="64b18-120">La proprietà Timestamp interna di Azure Cosmos DB (`_ts`) segue questo approccio.</span><span class="sxs-lookup"><span data-stu-id="64b18-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="64b18-121">È possibile utilizzare hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) classe tooserialize date e ore come numeri.</span><span class="sxs-lookup"><span data-stu-id="64b18-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="64b18-122">Indicizzazione dei valori DateTime per le query di intervallo</span><span class="sxs-lookup"><span data-stu-id="64b18-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="64b18-123">Le query di intervallo sono comuni con i valori DateTime.</span><span class="sxs-lookup"><span data-stu-id="64b18-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="64b18-124">Ad esempio, se è necessario toofind tutti gli ordini creati da ieri o trovare tutti gli ordini spediti in hello ultimi 5 minuti, è necessario tooperform le query di intervallo.</span><span class="sxs-lookup"><span data-stu-id="64b18-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="64b18-125">tooexecute queste query in modo efficiente, è necessario configurare la raccolta per l'indicizzazione intervallo sulle stringhe.</span><span class="sxs-lookup"><span data-stu-id="64b18-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="64b18-126">Ulteriori informazioni su tooconfigure criteri di indicizzazione [criteri di indicizzazione Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="64b18-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="64b18-127">Esecuzione di query per i valori DateTime in LINQ</span><span class="sxs-lookup"><span data-stu-id="64b18-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="64b18-128">Hello, DocumentDB .NET SDK supporta automaticamente l'esecuzione di query su dati archiviati nel database di Azure Cosmos tramite LINQ.</span><span class="sxs-lookup"><span data-stu-id="64b18-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="64b18-129">Ad esempio, hello frammento di codice seguente mostra una query LINQ che ordini i filtri che sono stati spediti in hello ultimi tre giorni.</span><span class="sxs-lookup"><span data-stu-id="64b18-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="64b18-130">Maggiori informazioni su Azure Cosmos DB SQL query language e hello provider LINQ in [l'esecuzione di query Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="64b18-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="64b18-131">In questo articolo è stato esaminato come toostore, indice e query date e ore in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="64b18-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64b18-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64b18-132">Next Steps</span></span>
* <span data-ttu-id="64b18-133">Scaricare ed eseguire hello [esempi su GitHub di codice](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="64b18-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="64b18-134">Altre informazioni sulle [query dell'API di DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="64b18-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="64b18-135">Altre informazioni sui [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="64b18-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
