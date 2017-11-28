---
title: Glossario di strumenti di Database aaaElastic | Documenti Microsoft
description: Spiegazione dei termini utilizzati per gli strumenti dei database elastici
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="8ed23-103">Glossario sugli strumenti di database elastici</span><span class="sxs-lookup"><span data-stu-id="8ed23-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="8ed23-104">Hello termini seguenti vengono definiti per hello [strumenti di Database elastico](sql-database-elastic-scale-introduction.md), una funzionalità di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed23-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="8ed23-105">strumenti Hello sono utilizzati toomanage [partizione viene mappata](sql-database-elastic-scale-shard-map-management.md)e includere hello [libreria client](sql-database-elastic-database-client-library.md), hello [strumento di merge di divisione](sql-database-elastic-scale-overview-split-and-merge.md), [pool elastici](sql-database-elastic-pool.md), e [query](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ed23-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="8ed23-106">Questi termini vengono utilizzati [aggiunta di una partizione utilizzando gli strumenti di Database elastico](sql-database-elastic-scale-add-a-shard.md) e [utilizzando i problemi di mappa partizioni toofix classe RecoveryManager hello](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8ed23-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Termini della scalabilità elastica][1]

<span data-ttu-id="8ed23-108">**Database**: un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed23-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="8ed23-109">**Routing dipendente dai dati**: hello funzionalità che consente una partizione di tooa tooconnect applicazione assegnata una chiave di partizionamento orizzontale specifica.</span><span class="sxs-lookup"><span data-stu-id="8ed23-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="8ed23-110">Vedere [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="8ed23-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="8ed23-111">Confrontare troppo**[Query più partizioni](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="8ed23-112">**Mappa partizioni globale**: hello mappa tra le chiavi di partizionamento orizzontale e i rispettive partizioni all'interno di un **set di partizioni**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="8ed23-113">mappa di partizioni globale Hello viene archiviata in hello **gestore mappe partizioni**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="8ed23-114">Confrontare troppo**mappa partizioni locali**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="8ed23-115">**Mappa partizioni di tipo elenco**: una mappa partizioni in cui le chiavi di partizionamento orizzontale vengono mappate singolarmente.</span><span class="sxs-lookup"><span data-stu-id="8ed23-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="8ed23-116">Confrontare troppo**mappa partizioni intervallo**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="8ed23-117">**Mappa partizioni locali**: archiviati in una partizione, mappa di partizioni locale hello contiene i mapping per gli shardlet hello che risiedono in partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="8ed23-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="8ed23-118">**Query su più partizioni**: hello possibilità tooissue una query su più partizioni; vengono restituiti i set di risultati utilizzando la semantica di UNION ALL (noto anche come "query fan-out").</span><span class="sxs-lookup"><span data-stu-id="8ed23-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="8ed23-119">Confrontare troppo**routing dipendente dai dati**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="8ed23-120">**Multi-tenant** e **Tenant singolo**: l'immagine mostra un database a tenant singolo e un database multi-tenant:</span><span class="sxs-lookup"><span data-stu-id="8ed23-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Database a tenant singolo e multi-tenant](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="8ed23-122">Ecco una rappresentazione di database a tenant singolo e multi-tenant **partizionati** .</span><span class="sxs-lookup"><span data-stu-id="8ed23-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Database a tenant singolo e multi-tenant](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="8ed23-124">**Mappa partizioni intervallo**: una mappa partizioni in cui hello strategia di distribuzione di partizioni si basa su più intervalli di valori contigui.</span><span class="sxs-lookup"><span data-stu-id="8ed23-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="8ed23-125">**Tabelle di riferimento**: tabelle che non vengono partizionate, ma vengono replicate tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="8ed23-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="8ed23-126">I codici di avviamento postale, ad esempio, possono essere archiviati in una tabella di riferimento.</span><span class="sxs-lookup"><span data-stu-id="8ed23-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="8ed23-127">**Partizione**: un database SQL di Azure che archivia i dati da un set di dati partizionato.</span><span class="sxs-lookup"><span data-stu-id="8ed23-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="8ed23-128">**Elasticità partizioni**: hello possibilità tooperform entrambi **scalabilità orizzontale** e **la scalabilità verticale**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="8ed23-129">**Tabelle partizionate**: tabelle che vengono partizionate, ovvero i cui dati vengono distribuiti tra le partizioni in base ai valori della chiave di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="8ed23-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="8ed23-130">**Chiave di partizionamento orizzontale**: un valore di colonna che determina la modalità di distribuzione dei dati tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="8ed23-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="8ed23-131">Hello tipo di valore può essere uno dei seguenti hello: **int**, **bigint**, **varbinary**, o **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="8ed23-132">**Set di partizioni**: hello raccolta di partizioni che sono con attributo toohello stessa mappa partizioni nel gestore mappe partizioni di hello.</span><span class="sxs-lookup"><span data-stu-id="8ed23-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="8ed23-133">**Shardlet**: tutti i dati di hello associati a un singolo valore di una chiave di partizionamento orizzontale in una partizione.</span><span class="sxs-lookup"><span data-stu-id="8ed23-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="8ed23-134">Un shardlet è hello più piccola unità di spostamento di dati possibili quando ridistribuzione di tabelle partizionate.</span><span class="sxs-lookup"><span data-stu-id="8ed23-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="8ed23-135">**Mappa partizioni**: hello set di mapping tra le chiavi di partizionamento orizzontale e i rispettive partizioni.</span><span class="sxs-lookup"><span data-stu-id="8ed23-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="8ed23-136">**Gestore mappe partizioni**: un archivio di oggetti e dati di gestione che contiene i mapping per uno o più set di partizioni, percorsi partizioni e alle mappe partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="8ed23-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mapping][2]

## <a name="verbs"></a><span data-ttu-id="8ed23-138">Verbi</span><span class="sxs-lookup"><span data-stu-id="8ed23-138">Verbs</span></span>
<span data-ttu-id="8ed23-139">**Scalabilità orizzontale**: act hello della scala (o) una raccolta di partizioni, aggiungendo o rimuovendo mappa partizioni tooa di partizioni, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8ed23-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Scalabilità orizzontale e verticale][3]

<span data-ttu-id="8ed23-141">**Merge**: azione hello lo spostamento degli shardlet dalla partizione tooone due partizioni e aggiornare di conseguenza mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="8ed23-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="8ed23-142">**Spostamento di Shardlet**: intende hello lo spostamento di una partizione diversa di tooa singolo shardlet.</span><span class="sxs-lookup"><span data-stu-id="8ed23-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="8ed23-143">**Partizioni**: atto hello di partizionamento orizzontale in modo identico dati strutturati tra più database in base a una chiave di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="8ed23-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="8ed23-144">**Split**: intende hello lo spostamento di shardlet diverse dalla partizione di una partizione tooanother (in genere nuovo).</span><span class="sxs-lookup"><span data-stu-id="8ed23-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="8ed23-145">Una chiave di partizionamento orizzontale viene fornita dall'utente hello come punto di divisione hello.</span><span class="sxs-lookup"><span data-stu-id="8ed23-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="8ed23-146">**Scalabilità verticale**: atto hello di scalare (verticale) hello livello delle prestazioni di una singola partizione.</span><span class="sxs-lookup"><span data-stu-id="8ed23-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="8ed23-147">Ad esempio, la modifica di una partizione da tooPremium Standard (che comporta più risorse di calcolo).</span><span class="sxs-lookup"><span data-stu-id="8ed23-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

