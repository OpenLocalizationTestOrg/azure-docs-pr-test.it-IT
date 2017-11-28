---
title: "Azure CosmosDB: unità richiesta al minuto (UR/m) | Microsoft Docs"
description: "Informazioni su come costo tooreduce utilizzando richieste unità al minuto."
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
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="02981-103">Unità richiesta al minuto in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="02981-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="02981-104">Azure DB Cosmos è progettato toohelp è ottenere un rapido e prevedibile prestazioni e scalabilità senza problemi con l'aumento delle dimensioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="02981-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="02981-105">È possibile effettuare il provisioning della velocità effettiva in un contenitore Cosmos DB sia con la granularità al secondo che con la granularità al minuto (UR/m).</span><span class="sxs-lookup"><span data-stu-id="02981-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="02981-106">velocità effettiva di provisioning con granularità al minuto Hello è usato toomanage imprevisti picchi di carico di lavoro hello che si verificano con una granularità al secondo.</span><span class="sxs-lookup"><span data-stu-id="02981-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="02981-107">In questo articolo viene fornita una panoramica del funzionamento di hello provisioning di unità di richiesta al minuto (UR/m).</span><span class="sxs-lookup"><span data-stu-id="02981-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="02981-108">obiettivo di Hello presente con il provisioning di UR/m è tooprovide un prestazioni prevedibili intorno esigenze imprevisti (in particolare se è necessario toorun analitica nella parte superiore in base ai dati) e i carichi di lavoro problemi.</span><span class="sxs-lookup"><span data-stu-id="02981-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="02981-109">Si vuole che i clienti utilizzano una velocità effettiva maggiore hello, che il provisioning in modo possibile scalare rapidamente con tranquillità toohave.</span><span class="sxs-lookup"><span data-stu-id="02981-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="02981-110">Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="02981-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="02981-111">Come funziona un'unità richiesta al minuto?</span><span class="sxs-lookup"><span data-stu-id="02981-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="02981-112">Qual è la differenza hello tra unità di richiesta al minuto e richieste al secondo?</span><span class="sxs-lookup"><span data-stu-id="02981-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="02981-113">Come tooprovision UR/m?</span><span class="sxs-lookup"><span data-stu-id="02981-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="02981-114">In quale scenario è opportuno considerare il provisioning di unità richiesta al minuto?</span><span class="sxs-lookup"><span data-stu-id="02981-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="02981-115">Come toouse hello toooptimize portale metriche personali costi e prestazioni?</span><span class="sxs-lookup"><span data-stu-id="02981-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="02981-116">Quale tipo di richiesta può utilizzare il budget UR/m?</span><span class="sxs-lookup"><span data-stu-id="02981-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="02981-117">Provisioning di unità richiesta al minuto (UR/m)</span><span class="sxs-lookup"><span data-stu-id="02981-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="02981-118">Quando si esegue il provisioning di Azure Cosmos DB granularità hello secondo (UR/sec), si ottiene garanzia hello che la richiesta ha esito positivo in una bassa latenza se la velocità effettiva non ha superato la capacità di hello provisioning all'interno di tale secondo.</span><span class="sxs-lookup"><span data-stu-id="02981-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="02981-119">Con UR/m, granularità hello è minuto hello con garanzia hello che la richiesta ha esito positivo all'interno di tale minuto.</span><span class="sxs-lookup"><span data-stu-id="02981-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="02981-120">Confronto toobursting sistemi, occorre assicurarsi prestazioni hello ottenuto sono prevedibile che è possibile pianificare su di esso.</span><span class="sxs-lookup"><span data-stu-id="02981-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="02981-121">Hello al minuto provisioning works è semplice:</span><span class="sxs-lookup"><span data-stu-id="02981-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="02981-122">UR/m viene addebitata ogni ora e in aggiunta tooRU/s.</span><span class="sxs-lookup"><span data-stu-id="02981-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="02981-123">Per altre informazioni, vedere la [pagina dei prezzi](https://aka.ms/acdbpricing) di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="02981-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="02981-124">Le UR/m possono essere abilitate a livello di raccolta,</span><span class="sxs-lookup"><span data-stu-id="02981-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="02981-125">Ciò può essere eseguito tramite hello SDK (Node.js, Java o .net) o tramite il portale di hello (includono anche i carichi di lavoro di MongoDB API)</span><span class="sxs-lookup"><span data-stu-id="02981-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="02981-126">Quando è abilitata UR/m, per ogni 100 UR/sec provisioning, è anche possibile ottenere 1.000 UR/m provisioning (rapporto hello è 10 x)</span><span class="sxs-lookup"><span data-stu-id="02981-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="02981-127">In un determinato secondo, un'unità richiesta utilizza il provisioning di UR/m solo se durante tale secondo è stato superato il provisioning al secondo</span><span class="sxs-lookup"><span data-stu-id="02981-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="02981-128">Una volta hello termina il periodo di 60 secondi (UTC), viene riempito hello per ogni minuto provisioning</span><span class="sxs-lookup"><span data-stu-id="02981-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="02981-129">Le UR/m possono essere abilitate solo per le raccolte con un provisioning massimo di 5.000 UR/s per partizione.</span><span class="sxs-lookup"><span data-stu-id="02981-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="02981-130">Se le esigenze di velocità effettiva aumentano e si ha un livello di provisioning per partizione così elevato, si riceverà un messaggio di avviso</span><span class="sxs-lookup"><span data-stu-id="02981-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="02981-131">Segue un esempio concreto, in cui un cliente può effettuare il provisioning di 10.000 UR/s con 100.000 UR/m, risparmiando il 73% sui costi rispetto al provisioning per picco (a 50.000 UR/sec) in un periodo di 90 secondi in una raccolta con un provisioning di 10.000 UR/s e 100.000 UR/m:</span><span class="sxs-lookup"><span data-stu-id="02981-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="02981-132">1 secondo: budget UR/m hello è impostato su 100.000</span><span class="sxs-lookup"><span data-stu-id="02981-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="02981-133">secondo 3a: durante la seconda hello consumo dell'unità richiesta è stata 11,010 russo, 1,010 RUs sopra il provisioning di hello UR/sec.</span><span class="sxs-lookup"><span data-stu-id="02981-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="02981-134">Quindi, 1,010 russo è detratto budget UR/m hello.</span><span class="sxs-lookup"><span data-stu-id="02981-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="02981-135">98,990 RUs sono disponibili per hello prossimi secondi 57 budget UR/m hello</span><span class="sxs-lookup"><span data-stu-id="02981-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="02981-136">secondo 29: durante il secondo, si è verificato un picco di grandi dimensioni (> 4 volte superiore rispetto al secondo di provisioning) e il consumo di hello dell'unità richiesta è stata 46,920 russo.</span><span class="sxs-lookup"><span data-stu-id="02981-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="02981-137">36,920 RUs vengono dedotti dal budget UR/m hello di eliminazione da 92,323 too55 RUs (secondo 28), 403 russo (29 secondi)</span><span class="sxs-lookup"><span data-stu-id="02981-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="02981-138">secondo 61st: budget UR/m viene ripristinata too100, russo 000.</span><span class="sxs-lookup"><span data-stu-id="02981-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Grafico che mostra il consumo di hello e il provisioning di Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="02981-140">Specifica della capacità delle unità richiesta con UR/M</span><span class="sxs-lookup"><span data-stu-id="02981-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="02981-141">Quando si crea una raccolta di Azure Cosmos DB, specificare il numero di hello di unità di richiesta al secondo (UR al secondo) si desidera riservato per l'insieme di hello.</span><span class="sxs-lookup"><span data-stu-id="02981-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="02981-142">È inoltre possibile decidere se si desidera RU tooadd al minuto.</span><span class="sxs-lookup"><span data-stu-id="02981-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="02981-143">Questa operazione può essere eseguita tramite hello portale o hello SDK.</span><span class="sxs-lookup"><span data-stu-id="02981-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="02981-144">Tramite hello portale</span><span class="sxs-lookup"><span data-stu-id="02981-144">Through hello Portal</span></span>

<span data-ttu-id="02981-145">Per abilitare o disabilitare UR al minuto, è sufficiente un clic durante il provisioning di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="02981-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Screenshot che mostra come tooset UR/m in hello portale di Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="02981-147">Tramite hello SDK</span><span class="sxs-lookup"><span data-stu-id="02981-147">Through hello SDK</span></span>
<span data-ttu-id="02981-148">In primo luogo, è importante toonote che UR/m è disponibile solo per hello seguenti SDK:</span><span class="sxs-lookup"><span data-stu-id="02981-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="02981-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="02981-149">.Net 1.14.0</span></span>
* <span data-ttu-id="02981-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="02981-150">Java 1.11.0</span></span>
* <span data-ttu-id="02981-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="02981-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="02981-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="02981-152">Python 2.2.0</span></span>

<span data-ttu-id="02981-153">Di seguito è riportato un frammento di codice per la creazione di una raccolta con 3.000 unità di richiesta per ogni unità di secondo e 30.000 richiesta al minuto utilizzando hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="02981-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="02981-154">Ecco un frammento di codice per la modifica di velocità effettiva di hello di una raccolta di too5, 000 unità di richiesta al secondo senza provisioning RU al minuto utilizzando hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="02981-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="02981-155">Scenari ideali</span><span class="sxs-lookup"><span data-stu-id="02981-155">Good fit scenarios</span></span>

<span data-ttu-id="02981-156">In questa sezione è disponibile una panoramica degli scenari ideali per abilitare le unità richiesta al minuto.</span><span class="sxs-lookup"><span data-stu-id="02981-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="02981-157">**Ambiente di sviluppo e test:** ideale.</span><span class="sxs-lookup"><span data-stu-id="02981-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="02981-158">Durante la fase di sviluppo hello, se si sta testando l'applicazione con diversi carichi di lavoro, UR/m possono offrire flessibilità hello in questa fase.</span><span class="sxs-lookup"><span data-stu-id="02981-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="02981-159">Durante la hello [emulatore](local-emulator.md) è tootest un ottimo strumento gratuito Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="02981-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="02981-160">Tuttavia se si desidera toostart in un ambiente cloud, si avrà una grande flessibilità con UR/m alle proprie esigenze di prestazioni ad hoc.</span><span class="sxs-lookup"><span data-stu-id="02981-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="02981-161">Sarà possibile dedicare più tempo allo sviluppo, non essendo più necessario preoccuparsi in primo luogo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="02981-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="02981-162">È consigliabile iniziare con provisioning hello minimo UR/sec e abilitare UR/m.</span><span class="sxs-lookup"><span data-stu-id="02981-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="02981-163">**Esigenze di granularità al minuto non prevedibili e di picco:** ideale. Risparmio: dal 25 al 75%.</span><span class="sxs-lookup"><span data-stu-id="02981-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="02981-164">Grazie alle UR/m sono stati osservati notevoli miglioramenti per la maggior parte degli scenari di produzione.</span><span class="sxs-lookup"><span data-stu-id="02981-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="02981-165">Se si dispone di un carico di lavoro IoT è picco più volte in un minuto, nel caso di query in esecuzione quando il sistema effettua massa inserire in hello stesso tempo, è necessario capacità aggiuntiva per esigenze di handeling problemi.</span><span class="sxs-lookup"><span data-stu-id="02981-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="02981-166">È consigliabile ottimizzare le esigenze delle risorse applicando l'approccio graduale indicato più avanti.</span><span class="sxs-lookup"><span data-stu-id="02981-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Grafico che illustra il consumo di richieste con una granularità di 5 minuti](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="02981-168">*Figura: benchmark del consumo di UR*</span><span class="sxs-lookup"><span data-stu-id="02981-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="02981-169">**Massima tranquillità:** ideale. Risparmio: dal 10 al 20%.</span><span class="sxs-lookup"><span data-stu-id="02981-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="02981-170">In alcuni casi, si desidera toohave tranquillità e non preoccuparsi picchi possibili e la limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="02981-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="02981-171">Questa funzionalità è hello right, uno per l'utente.</span><span class="sxs-lookup"><span data-stu-id="02981-171">This feature is hello right one for you.</span></span> <span data-ttu-id="02981-172">In questo caso, è consigliabile abilitare RU/m e ridurre leggermente il provisioning al secondo.</span><span class="sxs-lookup"><span data-stu-id="02981-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="02981-173">In questo caso è diverso da hello sopra come non si tenterà di toooptimize rapidamente il provisioning.</span><span class="sxs-lookup"><span data-stu-id="02981-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="02981-174">Non si tratta solo di eliminare le limitazioni.</span><span class="sxs-lookup"><span data-stu-id="02981-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="02981-175">Le operazioni critiche con esigenze ad hoc: in alcuni casi, è consigliabile tooonly consentire operazioni critiche accesso UR/m budget in modo da non ottenere budget hello consumare da ad hoc o meno operazioni importanti.</span><span class="sxs-lookup"><span data-stu-id="02981-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="02981-176">Che può essere facilmente definite nella sezione hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="02981-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="02981-177">Utilizzo di hello metriche portale toooptimize costi e prestazioni</span><span class="sxs-lookup"><span data-stu-id="02981-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="02981-178">**Nelle prossime settimane hello, si svilupperà ulteriormente il contenuto di hello intorno monitoraggio RUs consumo minuto toooptimize che richiede la velocità effettiva.**</span><span class="sxs-lookup"><span data-stu-id="02981-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="02981-179">Tramite le metriche del portale di hello, è possibile visualizzare la quantità di secondi di RU regolare utilizzi e RU minuti.</span><span class="sxs-lookup"><span data-stu-id="02981-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="02981-180">Il monitoraggio di queste metriche consente di ottimizzare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="02981-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="02981-181">È consigliabile un approccio dettagliate su come toouse vantaggio tooyour UR/m.</span><span class="sxs-lookup"><span data-stu-id="02981-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="02981-182">Per ogni passaggio, è necessario avere una panoramica del consumo di hello RU che rappresenta un ciclo completo del carico di lavoro (potrebbe essere ore, giorni, o persino settimane) e ottenere informazioni dettagliate sull'utilizzo di hello di il provisioning.</span><span class="sxs-lookup"><span data-stu-id="02981-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="02981-183">principio Hello dietro questo approccio è toomake il provisioning di velocità effettiva come chiudere come possibili tooa di provisioning che corrispondono ai criteri delle prestazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="02981-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![Grafico che illustra il consumo di richieste con una granularità di 5 minuti](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="02981-185">toounderstand hello ottimale provisioning punto per il carico di lavoro, è necessario toounderstand:</span><span class="sxs-lookup"><span data-stu-id="02981-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="02981-186">Modelli di consumo: spike prolungati, sporadici o inesistenti?</span><span class="sxs-lookup"><span data-stu-id="02981-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="02981-187">Spike di dimensioni piccole (2 volte la media), medie o grandi (più di 10 volte la media)?</span><span class="sxs-lookup"><span data-stu-id="02981-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="02981-188">Percentuale di richieste limitate: la presenza di qualche limitazione è accettabile?</span><span class="sxs-lookup"><span data-stu-id="02981-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="02981-189">Se sì, in quale percentuale?</span><span class="sxs-lookup"><span data-stu-id="02981-189">If so, by how much?</span></span> 

<span data-ttu-id="02981-190">Dopo aver individuato gli obiettivi sono, sarà in grado di tooget più vicino toohello ottimale di provisioning.</span><span class="sxs-lookup"><span data-stu-id="02981-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="02981-191">tooassist, desideriamo tooprovide un istruzioni generali sulle modalità toooptimize il provisioning in base all'utilizzo registrato UR/m.</span><span class="sxs-lookup"><span data-stu-id="02981-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="02981-192">Questa Guida non applica il tipo di tooall dei carichi di lavoro, ma si basa sulla conoscenza anteprima privata hello.</span><span class="sxs-lookup"><span data-stu-id="02981-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="02981-193">Tali linee guida potrebbero cambiare nel corso del tempo:</span><span class="sxs-lookup"><span data-stu-id="02981-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="02981-194">% utilizzo UR/m</span><span class="sxs-lookup"><span data-stu-id="02981-194">RU/m % utilization</span></span>|<span data-ttu-id="02981-195">Grado di utilizzo di UR/m</span><span class="sxs-lookup"><span data-stu-id="02981-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="02981-196">Azioni consigliate per il provisioning</span><span class="sxs-lookup"><span data-stu-id="02981-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="02981-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="02981-197">0-1%</span></span>|<span data-ttu-id="02981-198">Sottoutilizzo</span><span class="sxs-lookup"><span data-stu-id="02981-198">Under utilization</span></span>|<span data-ttu-id="02981-199">Abbassare di ulteriori UR/m tooconsume UR/sec</span><span class="sxs-lookup"><span data-stu-id="02981-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="02981-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="02981-200">1-10%</span></span>|<span data-ttu-id="02981-201">Uso appropriato</span><span class="sxs-lookup"><span data-stu-id="02981-201">Healthy use</span></span>|<span data-ttu-id="02981-202">Mantenere hello stesso provisioning livello</span><span class="sxs-lookup"><span data-stu-id="02981-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="02981-203">Più del 10%</span><span class="sxs-lookup"><span data-stu-id="02981-203">Above 10%</span></span>|<span data-ttu-id="02981-204">Sovrautilizzo</span><span class="sxs-lookup"><span data-stu-id="02981-204">Over utilization</span></span>|<span data-ttu-id="02981-205">Aumentare meno UR/m toorely UR/sec</span><span class="sxs-lookup"><span data-stu-id="02981-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="02981-206">Selezionare le operazioni che possono utilizzare budget UR/m hello</span><span class="sxs-lookup"><span data-stu-id="02981-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="02981-207">A livello di richiesta, è possibile anche abilitare/disabilitare UR/m tooserve hello preventivo indipendentemente dal tipo di operazione.</span><span class="sxs-lookup"><span data-stu-id="02981-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="02981-208">Se viene utilizzato regolare budget RUs/sec provisioning e richiesta hello non può utilizzare budget UR/m hello, verrà limitata la richiesta.</span><span class="sxs-lookup"><span data-stu-id="02981-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="02981-209">Per impostazione predefinita, qualsiasi richiesta viene gestita dal budget per le UR/m se il budget per la velocità effettiva di UR/m è attivato.</span><span class="sxs-lookup"><span data-stu-id="02981-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="02981-210">Di seguito è riportato un frammento di codice per la disabilitazione di budget UR/m utilizzando l'API DocumentDB hello per le operazioni CRUD e query.</span><span class="sxs-lookup"><span data-stu-id="02981-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="02981-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02981-211">Next steps</span></span>

<span data-ttu-id="02981-212">Questo articolo descrive come funziona il partizionamento in Azure Cosmos DB, come creare raccolte partizionate e come scegliere una chiave di partizione efficace per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="02981-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="02981-213">Eseguire il test delle prestazioni e della scalabilità con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="02981-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="02981-214">Per un esempio, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="02981-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="02981-215">Iniziare a scrivere codice con hello [SDK](documentdb-sdk-dotnet.md) o hello [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="02981-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="02981-216">Informazioni sulla [velocità effettiva di provisioning in Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="02981-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

