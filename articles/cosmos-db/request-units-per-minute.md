---
title: "Azure CosmosDB: unità richiesta al minuto (UR/m) | Microsoft Docs"
description: "Informazioni su come ridurre i costi utilizzando le unità richiesta al minuto."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="cfa1a-103">Unità richiesta al minuto in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cfa1a-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="cfa1a-104">Azure Cosmos DB è progettato per ottenere prestazioni rapide e prevedibili e per eseguire facilmente un ridimensionamento in base allo sviluppo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="cfa1a-105">È possibile effettuare il provisioning della velocità effettiva in un contenitore Cosmos DB sia con la granularità al secondo che con la granularità al minuto (UR/m).</span><span class="sxs-lookup"><span data-stu-id="cfa1a-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="cfa1a-106">La velocità effettiva con provisioning con granularità al minuto viene usata per gestire gli spike imprevisti nel carico di lavoro che si verificano con la granularità al secondo.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="cfa1a-107">Questo articolo offre una panoramica di come funziona il provisioning delle unità richiesta al minuto (UR/m).</span><span class="sxs-lookup"><span data-stu-id="cfa1a-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="cfa1a-108">L'obiettivo da raggiungere con il provisioning di UR/m è quello di garantire prestazioni prevedibili con esigenze imprevedibili (soprattutto se è necessario eseguire l'analisi sui dati operativi) e carichi di lavoro di picco.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="cfa1a-109">È importante che i clienti possano utilizzare maggiormente la velocità effettiva di cui effettuano il provisioning in modo che possano eseguire rapidamente e senza problemi un ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="cfa1a-110">Dopo la lettura di questo articolo, si potrà rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="cfa1a-111">Come funziona un'unità richiesta al minuto?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="cfa1a-112">Qual è la differenza tra unità richiesta al minuto e unità richiesta al secondo?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="cfa1a-113">Come effettuare il provisioning di UR/m?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-113">How to provision RU/m?</span></span>
* <span data-ttu-id="cfa1a-114">In quale scenario è opportuno considerare il provisioning di unità richiesta al minuto?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="cfa1a-115">Come usare le metriche del portale per ottimizzare i costi e le prestazioni?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="cfa1a-116">Quale tipo di richiesta può utilizzare il budget UR/m?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="cfa1a-117">Provisioning di unità richiesta al minuto (UR/m)</span><span class="sxs-lookup"><span data-stu-id="cfa1a-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="cfa1a-118">Quando si effettua il provisioning di Azure Cosmos DB con la granularità al secondo (UR/s), si ha la certezza che la richiesta abbia esito positivo a una bassa latenza se la velocità effettiva non ha superato la capacità di cui è stato effettuato il provisioning entro un secondo.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="cfa1a-119">Con le UR/m, la granularità è al minuto con la certezza che la richiesta abbia esito positivo entro un minuto.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="cfa1a-120">Rispetto ai sistemi burst, si ha la garanzia che le prestazioni ottenute siano prevedibili e affidabili.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="cfa1a-121">Il funzionamento del provisioning al minuto è semplice:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="cfa1a-122">Le UR/m vengono fatturate su base oraria e in aggiunta alle UR/s.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="cfa1a-123">Per altre informazioni, vedere la [pagina dei prezzi](https://aka.ms/acdbpricing) di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="cfa1a-124">Le UR/m possono essere abilitate a livello di raccolta,</span><span class="sxs-lookup"><span data-stu-id="cfa1a-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="cfa1a-125">tramite SDK (Node.js, Java o .Net) o tramite il portale (includere anche i carichi di lavoro con API MongoDB)</span><span class="sxs-lookup"><span data-stu-id="cfa1a-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="cfa1a-126">Quando le UR/m sono abilitate, per ogni 100 UR/s di cui viene effettuato il provisioning, viene effettuato il provisioning anche di 1.000 UR/m (il rapporto è di 10x)</span><span class="sxs-lookup"><span data-stu-id="cfa1a-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="cfa1a-127">In un determinato secondo, un'unità richiesta utilizza il provisioning di UR/m solo se durante tale secondo è stato superato il provisioning al secondo</span><span class="sxs-lookup"><span data-stu-id="cfa1a-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="cfa1a-128">Al termine del periodo di 60 secondi (UTC), il provisioning al minuto viene ricaricato</span><span class="sxs-lookup"><span data-stu-id="cfa1a-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="cfa1a-129">Le UR/m possono essere abilitate solo per le raccolte con un provisioning massimo di 5.000 UR/s per partizione.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="cfa1a-130">Se le esigenze di velocità effettiva aumentano e si ha un livello di provisioning per partizione così elevato, si riceverà un messaggio di avviso</span><span class="sxs-lookup"><span data-stu-id="cfa1a-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="cfa1a-131">Segue un esempio concreto, in cui un cliente può effettuare il provisioning di 10.000 UR/s con 100.000 UR/m, risparmiando il 73% sui costi rispetto al provisioning per picco (a 50.000 UR/sec) in un periodo di 90 secondi in una raccolta con un provisioning di 10.000 UR/s e 100.000 UR/m:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="cfa1a-132">1° secondo: il budget per UR/m è impostato su 100.000</span><span class="sxs-lookup"><span data-stu-id="cfa1a-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="cfa1a-133">3° secondo: durante tale secondo il consumo di unità richiesta è stato di 11.010 UR, 1.010 UR oltre il provisioning di UR/s.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="cfa1a-134">Vengono quindi dedotte 1.010 UR dal budget per UR/m.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="cfa1a-135">98.990 UR sono disponibili per i successivi 57 secondi nel budget per UR/m</span><span class="sxs-lookup"><span data-stu-id="cfa1a-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="cfa1a-136">29° secondo: durante tale secondo, si è verificato uno spike elevato (più di 4 volte maggiore del provisioning al secondo) e il consumo di unità richiesta è stato di 46.920 UR.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="cfa1a-137">36.920 UR vengono dedotte dal budget per UR/m che è sceso da 92.323 UR (28° secondo) a 55.403 UR (29° secondo)</span><span class="sxs-lookup"><span data-stu-id="cfa1a-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="cfa1a-138">61° secondo: il budget per UR/m viene di nuovo impostato su 100.000 UR.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![Grafico che illustra il consumo e il provisioning di Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="cfa1a-140">Specifica della capacità delle unità richiesta con UR/M</span><span class="sxs-lookup"><span data-stu-id="cfa1a-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="cfa1a-141">Quando si crea una raccolta di Azure Cosmos DB, si specifica il numero di unità richiesta al secondo da riservare per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="cfa1a-142">È anche possibile decidere se aggiungere UR al minuto.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="cfa1a-143">Questa operazione può essere eseguita tramite il portale o l'SDK.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="cfa1a-144">Tramite il portale</span><span class="sxs-lookup"><span data-stu-id="cfa1a-144">Through the Portal</span></span>

<span data-ttu-id="cfa1a-145">Per abilitare o disabilitare UR al minuto, è sufficiente un clic durante il provisioning di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Screenshot che illustra come impostare UR/m nel portale di Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="cfa1a-147">Tramite l'SDK</span><span class="sxs-lookup"><span data-stu-id="cfa1a-147">Through the SDK</span></span>
<span data-ttu-id="cfa1a-148">Prima di tutto, è importante notare che UR/m è disponibile solo per gli SDK seguenti:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="cfa1a-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="cfa1a-149">.Net 1.14.0</span></span>
* <span data-ttu-id="cfa1a-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="cfa1a-150">Java 1.11.0</span></span>
* <span data-ttu-id="cfa1a-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="cfa1a-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="cfa1a-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="cfa1a-152">Python 2.2.0</span></span>

<span data-ttu-id="cfa1a-153">Ecco un frammento di codice per la creazione di una raccolta con 3.000 unità richiesta al secondo e 30.000 unità richiesta al minuto usando .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="cfa1a-154">Ecco un frammento di codice per la modifica della velocità effettiva di una raccolta fino a 5.000 unità richiesta al secondo senza provisioning di UR al minuto usando .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="cfa1a-155">Scenari ideali</span><span class="sxs-lookup"><span data-stu-id="cfa1a-155">Good fit scenarios</span></span>

<span data-ttu-id="cfa1a-156">In questa sezione è disponibile una panoramica degli scenari ideali per abilitare le unità richiesta al minuto.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="cfa1a-157">**Ambiente di sviluppo e test:** ideale.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="cfa1a-158">Durante la fase di sviluppo, se si testa l'applicazione con carichi di lavoro diversi, UR/m può offrire la flessibilità necessaria.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="cfa1a-159">L'[emulatore](local-emulator.md) è invece un ottimo strumento gratuito per testare Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="cfa1a-160">Se tuttavia si preferisce iniziare in un ambiente cloud, UR/m offrirà una flessibilità elevata in termini di prestazioni ad hoc.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="cfa1a-161">Sarà possibile dedicare più tempo allo sviluppo, non essendo più necessario preoccuparsi in primo luogo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="cfa1a-162">È consigliabile iniziare con il provisioning di UR/s minimo e abilitare UR/m.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="cfa1a-163">**Esigenze di granularità al minuto non prevedibili e di picco:** ideale. Risparmio: dal 25 al 75%.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="cfa1a-164">Grazie alle UR/m sono stati osservati notevoli miglioramenti per la maggior parte degli scenari di produzione.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="cfa1a-165">Se è presente un carico di lavoro IoT in cui si verifica uno spike alcune volte in un minuto, se sono in esecuzione query quando il sistema esegue un inserimento di massa nello stesso momento, sarà necessaria capacità aggiuntiva per gestire le esigenze di picco.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="cfa1a-166">È consigliabile ottimizzare le esigenze delle risorse applicando l'approccio graduale indicato più avanti.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Grafico che illustra il consumo di richieste con una granularità di 5 minuti](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="cfa1a-168">*Figura: benchmark del consumo di UR*</span><span class="sxs-lookup"><span data-stu-id="cfa1a-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="cfa1a-169">**Massima tranquillità:** ideale. Risparmio: dal 10 al 20%.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="cfa1a-170">A volte l'obiettivo è semplicemente quello di lavorare in tranquillità, senza preoccuparsi di potenziali picchi e limitazioni.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="cfa1a-171">Questa funzionalità è l'ideale.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-171">This feature is the right one for you.</span></span> <span data-ttu-id="cfa1a-172">In questo caso, è consigliabile abilitare RU/m e ridurre leggermente il provisioning al secondo.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="cfa1a-173">Questo caso è diverso da quello precedente perché non si cercherà di ottimizzare il provisioning in modo aggressivo.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="cfa1a-174">Non si tratta solo di eliminare le limitazioni.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="cfa1a-175">Operazioni critiche con esigenze ad hoc: a volte è consigliabile consentire solo alle operazioni critiche di accedere al budget per le UR/m in modo che il budget non venga utilizzato da operazioni ad hoc o meno importanti.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="cfa1a-176">Questa impostazione è facilmente definibile nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="cfa1a-177">Uso delle metriche del portale per ottimizzare i costi e le prestazioni</span><span class="sxs-lookup"><span data-stu-id="cfa1a-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="cfa1a-178">**Nelle prossime settimane, i contenuti sul monitoraggio del consumo al minuto di UR per ottimizzare le esigenze di velocità effettiva verrà integrato e aggiornato.**</span><span class="sxs-lookup"><span data-stu-id="cfa1a-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="cfa1a-179">Tramite le metriche del portale, è possibile visualizzare la quantità di normali secondi di UR utilizzata rispetto ai minuti di UR.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="cfa1a-180">Il monitoraggio di queste metriche consente di ottimizzare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="cfa1a-181">È consigliabile adottare un approccio graduale all'uso delle UR/m poterne sfruttare meglio i vantaggi.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="cfa1a-182">Per ogni passaggio, è consigliabile avere una panoramica del consumo di UR che rappresenti un ciclo completo del carico di lavoro (può trattarsi di giorni, ore o anche settimane) e ottenere informazioni dettagliate sull'utilizzo di ciò di cui viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="cfa1a-183">Il principio alla base di questo approccio è quello di far coincidere il più possibile il provisioning della velocità effettiva con un punto di provisioning corrispondente ai criteri delle prestazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![Grafico che illustra il consumo di richieste con una granularità di 5 minuti](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="cfa1a-185">Per individuare il punto di provisioning ottimale per il carico di lavoro, è necessario conoscere:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="cfa1a-186">Modelli di consumo: spike prolungati, sporadici o inesistenti?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="cfa1a-187">Spike di dimensioni piccole (2 volte la media), medie o grandi (più di 10 volte la media)?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="cfa1a-188">Percentuale di richieste limitate: la presenza di qualche limitazione è accettabile?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="cfa1a-189">Se sì, in quale percentuale?</span><span class="sxs-lookup"><span data-stu-id="cfa1a-189">If so, by how much?</span></span> 

<span data-ttu-id="cfa1a-190">Dopo avere identificato gli obiettivi, sarà possibile avvicinarsi al provisioning ottimale.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="cfa1a-191">Per assistere l'utente, vengono date indicazioni generali su come ottimizzare il provisioning in base al consumo di UR/m.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="cfa1a-192">Queste indicazioni non si applicano a tutti i tipi di carichi di lavoro, ma si basano sulle informazioni dell'anteprima privata.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="cfa1a-193">Tali linee guida potrebbero cambiare nel corso del tempo:</span><span class="sxs-lookup"><span data-stu-id="cfa1a-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="cfa1a-194">% utilizzo UR/m</span><span class="sxs-lookup"><span data-stu-id="cfa1a-194">RU/m % utilization</span></span>|<span data-ttu-id="cfa1a-195">Grado di utilizzo di UR/m</span><span class="sxs-lookup"><span data-stu-id="cfa1a-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="cfa1a-196">Azioni consigliate per il provisioning</span><span class="sxs-lookup"><span data-stu-id="cfa1a-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="cfa1a-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="cfa1a-197">0-1%</span></span>|<span data-ttu-id="cfa1a-198">Sottoutilizzo</span><span class="sxs-lookup"><span data-stu-id="cfa1a-198">Under utilization</span></span>|<span data-ttu-id="cfa1a-199">Ridurre le UR/s per utilizzare più UR/m</span><span class="sxs-lookup"><span data-stu-id="cfa1a-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="cfa1a-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="cfa1a-200">1-10%</span></span>|<span data-ttu-id="cfa1a-201">Uso appropriato</span><span class="sxs-lookup"><span data-stu-id="cfa1a-201">Healthy use</span></span>|<span data-ttu-id="cfa1a-202">Mantenere lo stesso livello di provisioning</span><span class="sxs-lookup"><span data-stu-id="cfa1a-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="cfa1a-203">Più del 10%</span><span class="sxs-lookup"><span data-stu-id="cfa1a-203">Above 10%</span></span>|<span data-ttu-id="cfa1a-204">Sovrautilizzo</span><span class="sxs-lookup"><span data-stu-id="cfa1a-204">Over utilization</span></span>|<span data-ttu-id="cfa1a-205">Aumentare le UR/s per ridurre l'uso delle UR/m</span><span class="sxs-lookup"><span data-stu-id="cfa1a-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="cfa1a-206">Selezionare le operazioni che possono utilizzare il budget per le UR/m</span><span class="sxs-lookup"><span data-stu-id="cfa1a-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="cfa1a-207">A livello di richiesta, è anche possibile abilitare/disabilitare il budget per le UR/m per poter gestire le richieste indipendentemente dal tipo di operazione.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="cfa1a-208">Se il normale budget per le UR/sec con provisioning viene esaurito e la richiesta non può utilizzare il budget per le UR/m, la richiesta verrà limitata.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="cfa1a-209">Per impostazione predefinita, qualsiasi richiesta viene gestita dal budget per le UR/m se il budget per la velocità effettiva di UR/m è attivato.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="cfa1a-210">Ecco un frammento di codice per disabilitare il budget per le UR/m usando l'API DocumentDB per le operazioni CRUD e di query.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="cfa1a-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cfa1a-211">Next steps</span></span>

<span data-ttu-id="cfa1a-212">Questo articolo descrive come funziona il partizionamento in Azure Cosmos DB, come creare raccolte partizionate e come scegliere una chiave di partizione efficace per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="cfa1a-213">Eseguire il test delle prestazioni e della scalabilità con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cfa1a-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="cfa1a-214">Per un esempio, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="cfa1a-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="cfa1a-215">Introduzione alla programmazione con gli [SDK](documentdb-sdk-dotnet.md) o l'[API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="cfa1a-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="cfa1a-216">Informazioni sulla [velocità effettiva di provisioning in Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="cfa1a-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

