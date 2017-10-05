---
title: "Test delle prestazioni e della scalabilità in Azure Cosmos DB | Microsoft Docs"
description: "Informazioni sull'esecuzione di test delle prestazioni e della scalabilità con Azure Cosmos DB"
keywords: test delle prestazioni
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="cacf7-104">Test delle prestazioni e della scalabilità con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cacf7-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="cacf7-105">Il test delle prestazioni e della scalabilità è un passaggio chiave nello sviluppo di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cacf7-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="cacf7-106">Per molte applicazioni, il livello del database ha un impatto significativo sulle prestazioni e sulla scalabilità globali, è pertanto un componente fondamentale del test delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cacf7-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="cacf7-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) è appositamente progettato per garantire scalabilità elastica e prestazioni prevedibili ed è quindi ideale per applicazioni che richiedono un livello database con prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="cacf7-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="cacf7-108">Questo articolo offre informazioni di riferimento per gli sviluppatori che implementano gruppi di test delle prestazioni per i carichi di lavoro di Cosmos DB o valutano Cosmos DB per scenari di applicazioni ad alte prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cacf7-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="cacf7-109">Approfondisce soprattutto i test isolati delle prestazioni del database, ma include anche le procedure consigliate per le applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="cacf7-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="cacf7-110">Dopo la lettura di questo articolo, si potrà rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="cacf7-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="cacf7-111">Dove è possibile trovare un'applicazione client .NET di esempio per i test delle prestazioni di Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="cacf7-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="cacf7-112">Come è possibile ottenere livelli di velocità effettiva elevati con Cosmos DB dall'applicazione client?</span><span class="sxs-lookup"><span data-stu-id="cacf7-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="cacf7-113">Per iniziare a usare il codice, scaricare il progetto dell'[esempio relativo al test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="cacf7-113">To get started with code, please download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="cacf7-114">L'obiettivo di questa applicazione è illustrare le procedure consigliate per ottenere prestazioni migliori da Cosmos DB con un numero ridotto di computer client.</span><span class="sxs-lookup"><span data-stu-id="cacf7-114">The goal of this application is to demonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="cacf7-115">L'applicazione non è stata realizzata per dimostrare la capacità massima del servizio, che può essere aumentata senza limiti.</span><span class="sxs-lookup"><span data-stu-id="cacf7-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="cacf7-116">Se si è interessati alle opzioni di configurazione lato client per migliorare le prestazioni di Cosmos DB, vedere [Suggerimenti sulle prestazioni per Azure Cosmos DB](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="cacf7-116">If you're looking for client-side configuration options to improve Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="cacf7-117">Eseguire l'applicazione per il test delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="cacf7-117">Run the performance testing application</span></span>
<span data-ttu-id="cacf7-118">Il modo più rapido per iniziare è compilare ed eseguire l'esempio .NET riportato di seguito, come descritto nella procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="cacf7-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="cacf7-119">È anche possibile esaminare il codice sorgente e implementare configurazioni analoghe alle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="cacf7-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="cacf7-120">**Passaggio 1**: scaricare il progetto dell'[esempio relativo al test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark) o creare la biforcazione del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="cacf7-120">**Step 1:** Download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="cacf7-121">**Passaggio 2** : modificare le impostazioni di EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (facoltativo) nel file App.config.</span><span class="sxs-lookup"><span data-stu-id="cacf7-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="cacf7-122">Prima del provisioning delle raccolte con velocità effettiva elevata, consultare la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/) per stimare i costi di ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="cacf7-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="cacf7-123">Poiché l'addebito dello spazio di archiviazione e della velocità effettiva per Azure Cosmos DB viene eseguito in modo indipendente su base oraria, è possibile risparmiare eliminando o riducendo la velocità effettiva delle raccolte Azure Cosmos DB al termine del test.</span><span class="sxs-lookup"><span data-stu-id="cacf7-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="cacf7-124">**Passaggio 3** : compilare ed eseguire l'app console dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="cacf7-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="cacf7-125">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cacf7-125">You should see output like the following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="cacf7-126">**Passaggio 4 (se necessario)** : la velocità effettiva segnalata (UR/sec) dallo strumento deve essere analoga o superiore a quella della raccolta.</span><span class="sxs-lookup"><span data-stu-id="cacf7-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="cacf7-127">In caso contrario, l'aumento di DegreeOfParallelism in incrementi ridotti può aiutare a raggiungere il limite.</span><span class="sxs-lookup"><span data-stu-id="cacf7-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="cacf7-128">Se la velocità effettiva dall'app client su stabilizza, l'avvio di più istanze dell'app nelle stesse macchine o in macchine diverse consente di raggiungere il limite di provisioning tra istanze diverse.</span><span class="sxs-lookup"><span data-stu-id="cacf7-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="cacf7-129">Per ottenere assistenza per questo passaggio, inviare un messaggio di posta elettronica all'indirizzo askcosmosdb@microsoft.com o creare un ticket di supporto dal [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cacf7-129">If you need help with this step, please, write an email to askcosmosdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="cacf7-130">Quando l'app è in esecuzione, è possibile provare diversi [criteri di indicizzazione](indexing-policies.md) e [livelli di coerenza](consistency-levels.md) per comprenderne l'impatto sulla velocità effettiva e sulla latenza.</span><span class="sxs-lookup"><span data-stu-id="cacf7-130">Once you have the app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="cacf7-131">È anche possibile esaminare il codice sorgente e implementare configurazioni analoghe alle suite di test o alle applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="cacf7-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cacf7-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cacf7-132">Next steps</span></span>
<span data-ttu-id="cacf7-133">In questo articolo è stato illustrato come eseguire test delle prestazioni e della scalabilità con Cosmos DB usando un'app console .NET.</span><span class="sxs-lookup"><span data-stu-id="cacf7-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="cacf7-134">Per altre informazioni sull'uso di Azure Cosmos DB, vedere i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="cacf7-134">Please refer to the links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="cacf7-135">Esempio di test delle prestazioni di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cacf7-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="cacf7-136">Opzioni di configurazione client per migliorare le prestazioni di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cacf7-136">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="cacf7-137">Partizionamento lato server in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cacf7-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


