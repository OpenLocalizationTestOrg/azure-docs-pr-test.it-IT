---
title: Uso delle date in Azure Cosmos DB | Microsoft Docs
description: Informazioni sull'uso delle date in Azure Cosmos DB.
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
ms.openlocfilehash: b6a77e33eea24000037ffb31d7aae3cb1d345ce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="79ed4-103">Uso delle date in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79ed4-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="79ed4-104">Azure Cosmos DB offre flessibilità dello schema e un'indicizzazione avanzata tramite un modello di dati [JSON](http://www.json.org) nativo.</span><span class="sxs-lookup"><span data-stu-id="79ed4-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="79ed4-105">Tutte le risorse di Azure Cosmos DB, inclusi database, raccolte, documenti e procedure archiviate, sono modellate e archiviate come documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="79ed4-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="79ed4-106">Come requisito per essere portatile, JSON, insieme a Azure Cosmos DB, supporta solo un piccolo set di tipi di base: String, Number, Boolean, Array, Object e Null.</span><span class="sxs-lookup"><span data-stu-id="79ed4-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="79ed4-107">Tuttavia, JSON è flessibile e consente a sviluppatori e strutture di rappresentare tipi più complessi tramite l'uso di queste primitive, componendole come oggetti o matrici.</span><span class="sxs-lookup"><span data-stu-id="79ed4-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="79ed4-108">Oltre ai tipi di base, molte applicazioni hanno bisogno del tipo [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) per rappresentare date e timestamp.</span><span class="sxs-lookup"><span data-stu-id="79ed4-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span></span> <span data-ttu-id="79ed4-109">Questo articolo descrive come gli sviluppatori possono archiviare, recuperare ed eseguire query di date in Azure Cosmos DB usando .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="79ed4-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="79ed4-110">Archiviazione di valori DateTime</span><span class="sxs-lookup"><span data-stu-id="79ed4-110">Storing DateTimes</span></span>
<span data-ttu-id="79ed4-111">Per impostazione predefinita, [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializza i valori DateTime come stringhe [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874).</span><span class="sxs-lookup"><span data-stu-id="79ed4-111">By default, the [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="79ed4-112">La maggior parte delle applicazioni può usare la rappresentazione predefinita della stringa per il valore DateTime, per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="79ed4-112">Most applications can use the default string representation for DateTime for the following reasons:</span></span>

* <span data-ttu-id="79ed4-113">Le stringhe possono essere confrontate e l'ordinamento relativo dei valori DateTime viene conservato quando questi vengono trasformati in stringhe.</span><span class="sxs-lookup"><span data-stu-id="79ed4-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span></span> 
* <span data-ttu-id="79ed4-114">Questo approccio non richiede codici o attributi personalizzati per la conversione JSON.</span><span class="sxs-lookup"><span data-stu-id="79ed4-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="79ed4-115">Le date così come archiviate in JSON sono leggibili dall'utente.</span><span class="sxs-lookup"><span data-stu-id="79ed4-115">The dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="79ed4-116">Questo approccio può sfruttare l'indicizzazione di Azure Cosmos DB per query più veloci.</span><span class="sxs-lookup"><span data-stu-id="79ed4-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="79ed4-117">Ad esempio, il frammento seguente memorizza come documento un oggetto `Order` che contiene due proprietà DateTime, `ShipDate` e `OrderDate`, tramite .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="79ed4-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span></span>

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

<span data-ttu-id="79ed4-118">Il documento viene archiviato in Azure Cosmos DB come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="79ed4-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="79ed4-119">In alternativa, è possibile archiviare valori DateTime come timestamp Unix, ovvero come un numero che rappresenti i secondi trascorsi a partire dal 1° gennaio 1970.</span><span class="sxs-lookup"><span data-stu-id="79ed4-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="79ed4-120">La proprietà Timestamp interna di Azure Cosmos DB (`_ts`) segue questo approccio.</span><span class="sxs-lookup"><span data-stu-id="79ed4-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="79ed4-121">È possibile usare la classe [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) per serializzare come numeri i valori DateTime.</span><span class="sxs-lookup"><span data-stu-id="79ed4-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="79ed4-122">Indicizzazione dei valori DateTime per le query di intervallo</span><span class="sxs-lookup"><span data-stu-id="79ed4-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="79ed4-123">Le query di intervallo sono comuni con i valori DateTime.</span><span class="sxs-lookup"><span data-stu-id="79ed4-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="79ed4-124">Ad esempio, sono necessarie per trovare tutti gli ordini creati dal giorno precedente o tutti gli ordini spediti negli ultimi cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="79ed4-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span></span> <span data-ttu-id="79ed4-125">Per eseguire queste query in modo efficiente, è necessario configurare la raccolta per l'indicizzazione di intervallo nelle stringhe.</span><span class="sxs-lookup"><span data-stu-id="79ed4-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="79ed4-126">Per altre informazioni su come configurare i criteri di indicizzazione, vedere i [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="79ed4-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="79ed4-127">Esecuzione di query per i valori DateTime in LINQ</span><span class="sxs-lookup"><span data-stu-id="79ed4-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="79ed4-128">DocumentDB .NET SDK supporta automaticamente le query sui dati archiviati in Azure Cosmos DB tramite LINQ.</span><span class="sxs-lookup"><span data-stu-id="79ed4-128">The DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="79ed4-129">Ad esempio, il frammento seguente mostra una query LINQ che filtra gli ordini inviati negli ultimi tre giorni.</span><span class="sxs-lookup"><span data-stu-id="79ed4-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated to the following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="79ed4-130">Per altre informazioni sul linguaggio di query SQL di Azure Cosmos DB e sul provider LINQ, vedere l'[esecuzione di query in Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="79ed4-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="79ed4-131">In questo articolo è stato descritto come archiviare, indicizzare ed eseguire query per valori DateTime in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79ed4-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79ed4-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79ed4-132">Next Steps</span></span>
* <span data-ttu-id="79ed4-133">Scaricare ed eseguire gli [Esempi di codice su GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="79ed4-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="79ed4-134">Altre informazioni sulle [query dell'API di DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="79ed4-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="79ed4-135">Altre informazioni sui [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="79ed4-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
