---
title: esercitazione di distribuzione globale aaaAzure DB Cosmos per tabella API | Documenti Microsoft
description: Informazioni su come distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API di tabella.
services: cosmos-db
keywords: Distribuzione globale, Table
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="6753b-104">La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello tabella API</span><span class="sxs-lookup"><span data-stu-id="6753b-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="6753b-105">In questo articolo viene illustrata come toouse hello distribuzione globale di Azure Cosmos DB toosetup portale Azure e quindi connettersi utilizzando hello tabella API (anteprima).</span><span class="sxs-lookup"><span data-stu-id="6753b-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="6753b-106">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="6753b-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6753b-107">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6753b-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="6753b-108">Configurare la distribuzione globale mediante hello [tabella API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6753b-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="6753b-109">Connessione area geografica preferita tooa utilizzando hello tabella API</span><span class="sxs-lookup"><span data-stu-id="6753b-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="6753b-110">In ordine tootake sfruttare la [distribuzione globale](distribute-data-globally.md), applicazioni client possono specificare hello ordinato l'elenco delle preferenze di aree toobe utilizzato tooperform documento operazioni.</span><span class="sxs-lookup"><span data-stu-id="6753b-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="6753b-111">Questa operazione può essere eseguita dall'impostazione hello `TablePreferredLocations` il valore di configurazione nel file di configurazione app hello per l'anteprima di hello Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="6753b-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="6753b-112">Basato sulla configurazione dell'account Azure Cosmos DB hello, disponibilità internazionali corrente ed elenco preferenza hello specificato, verrà scelta la maggior parte degli endpoint ottimale da hello Azure Storage SDK tooperform hello scrivere e operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="6753b-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="6753b-113">Hello `TablePreferredLocations` deve contenere un elenco delimitato da virgole di indirizzi (multihosting) preferiti per le letture.</span><span class="sxs-lookup"><span data-stu-id="6753b-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="6753b-114">Ogni istanza del client è possibile specificare un subset di queste aree nell'ordine preferito hello per le letture di bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="6753b-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="6753b-115">aree Hello devono essere denominate con i relativi [i nomi visualizzati](https://msdn.microsoft.com/library/azure/gg441293.aspx), ad esempio, `West US`.</span><span class="sxs-lookup"><span data-stu-id="6753b-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="6753b-116">Tutte le letture che verranno inviate toohello prima area disponibile in hello `TablePreferredLocations` elenco.</span><span class="sxs-lookup"><span data-stu-id="6753b-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="6753b-117">Se hello richiesta non riesce, il client hello esito negativo all'area di hello elenco toohello successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="6753b-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="6753b-118">Hello SDK tenterà solo tooread dalle aree hello specificato in `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="6753b-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="6753b-119">In tal caso, ad esempio, se hello Account del Database è disponibile in tre aree, ma il client di hello specifica solo due delle hello non scrittura aree per `TablePreferredLocations`, quindi non verranno utilizzate alcun letture fuori area scrittura hello, anche nel caso di hello di failover.</span><span class="sxs-lookup"><span data-stu-id="6753b-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="6753b-120">Hello SDK invierà automaticamente area scrittura di tutte le operazioni di scrittura toohello corrente.</span><span class="sxs-lookup"><span data-stu-id="6753b-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="6753b-121">Se hello `TablePreferredLocations` non è impostata, verranno utilizzate dall'area di scrittura corrente hello tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="6753b-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="6753b-122">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="6753b-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="6753b-123">È possibile ottenere informazioni come toomanage hello la coerenza dell'account di replicato globalmente leggendo [livelli di coerenza nel database di Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6753b-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="6753b-124">Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="6753b-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6753b-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6753b-125">Next steps</span></span>

<span data-ttu-id="6753b-126">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="6753b-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6753b-127">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6753b-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="6753b-128">Configurare la distribuzione globale mediante hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="6753b-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="6753b-129">È ora possibile procedere toolearn esercitazione successiva toohello come toodevelop localmente tramite hello emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6753b-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6753b-130">Sviluppare in locale con emulator hello</span><span class="sxs-lookup"><span data-stu-id="6753b-130">Develop locally with hello emulator</span></span>](local-emulator.md)
