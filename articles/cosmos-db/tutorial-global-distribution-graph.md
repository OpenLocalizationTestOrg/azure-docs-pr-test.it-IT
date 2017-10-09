---
title: esercitazione di distribuzione globale Cosmos DB aaaAzure per l'API Graph | Documenti Microsoft
description: Informazioni su come distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API Graph.
services: cosmos-db
keywords: distribuzione globale, graph, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="c9f10-104">La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API Graph</span><span class="sxs-lookup"><span data-stu-id="c9f10-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="c9f10-105">In questo articolo viene illustrata come toouse hello distribuzione globale di Azure Cosmos DB toosetup portale Azure e quindi connettersi utilizzando hello API Graph (anteprima).</span><span class="sxs-lookup"><span data-stu-id="c9f10-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="c9f10-106">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="c9f10-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c9f10-107">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c9f10-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c9f10-108">Configurare la distribuzione globale mediante hello [sulle API Graph](graph-introduction.md) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="c9f10-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="c9f10-109">La connessione usando l'API Graph hello mediante .NET SDK hello la regione preferita tooa</span><span class="sxs-lookup"><span data-stu-id="c9f10-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="c9f10-110">API Graph Hello viene esposto come una libreria di estensione su hello DocumentDB SDK.</span><span class="sxs-lookup"><span data-stu-id="c9f10-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="c9f10-111">In ordine tootake sfruttare la [distribuzione globale](distribute-data-globally.md), applicazioni client possono specificare hello ordinato l'elenco delle preferenze di aree toobe utilizzato tooperform documento operazioni.</span><span class="sxs-lookup"><span data-stu-id="c9f10-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="c9f10-112">Questa operazione può essere eseguita mediante l'impostazione di criteri di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="c9f10-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="c9f10-113">Basato sulla configurazione dell'account Azure Cosmos DB hello, elenco delle preferenze hello e la disponibilità di internazionale corrente specificato, hello la maggior parte degli endpoint ottimale verrà scelto dal scrittura tooperform SDK di hello e operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="c9f10-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="c9f10-114">L'elenco delle preferenze viene specificato durante l'inizializzazione di una connessione tramite hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c9f10-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="c9f10-115">Hello SDK di accettare un parametro facoltativo "PreferredLocations" che rappresenta un elenco ordinato di aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f10-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="c9f10-116">**Scrive**: hello SDK invierà automaticamente tutti scrive toohello area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="c9f10-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="c9f10-117">**Legge**: tutte le letture verranno inviate toohello prima area disponibile nell'elenco PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="c9f10-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="c9f10-118">Se hello richiesta non riesce, il client hello esito negativo all'area di hello elenco toohello successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="c9f10-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="c9f10-119">Hello SDK tenterà solo tooread dalle aree hello specificato in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="c9f10-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="c9f10-120">In tal caso, ad esempio, se hello Cosmos DB account è disponibile in tre aree, ma client hello specifica solo due delle aree non scrittura hello per PreferredLocations, quindi non letture verranno utilizzate fuori area scrittura hello, anche nel caso di hello di failover.</span><span class="sxs-lookup"><span data-stu-id="c9f10-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="c9f10-121">un'applicazione Hello possibile verificare l'endpoint di scrittura corrente hello e leggere endpoint scelto da hello SDK dal controllo due proprietà, WriteEndpoint e ReadEndpoint, disponibili nella versione SDK 1.8 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c9f10-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="c9f10-122">Se non è impostata la proprietà PreferredLocations hello, verranno utilizzate dall'area di scrittura corrente hello tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="c9f10-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="c9f10-123">Utilizzo di hello SDK</span><span class="sxs-lookup"><span data-stu-id="c9f10-123">Using hello SDK</span></span>

<span data-ttu-id="c9f10-124">Ad esempio, hello .NET SDK, hello `ConnectionPolicy` parametro per hello `DocumentClient` costruttore ha una proprietà denominata `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="c9f10-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="c9f10-125">Questa proprietà può essere impostata tooa elenco di nomi di area.</span><span class="sxs-lookup"><span data-stu-id="c9f10-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="c9f10-126">nomi visualizzati Hello per [aree di Azure] [ regions] può essere specificato come parte di `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="c9f10-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="c9f10-127">Hello URL per gli endpoint di hello non deve essere considerato come costanti di lunga durate.</span><span class="sxs-lookup"><span data-stu-id="c9f10-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="c9f10-128">servizio Hello può aggiornare questi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c9f10-128">hello service may update these at any point.</span></span> <span data-ttu-id="c9f10-129">Hello SDK gestisce automaticamente questa modifica.</span><span class="sxs-lookup"><span data-stu-id="c9f10-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="c9f10-130">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="c9f10-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="c9f10-131">È possibile ottenere informazioni come toomanage hello la coerenza dell'account di replicato globalmente leggendo [livelli di coerenza nel database di Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="c9f10-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="c9f10-132">Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="c9f10-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9f10-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9f10-133">Next steps</span></span>

<span data-ttu-id="c9f10-134">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c9f10-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c9f10-135">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c9f10-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c9f10-136">Configurare la distribuzione globale mediante hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c9f10-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="c9f10-137">È ora possibile procedere toolearn esercitazione successiva toohello come toodevelop localmente tramite hello emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c9f10-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c9f10-138">Sviluppare in locale con emulator hello</span><span class="sxs-lookup"><span data-stu-id="c9f10-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

