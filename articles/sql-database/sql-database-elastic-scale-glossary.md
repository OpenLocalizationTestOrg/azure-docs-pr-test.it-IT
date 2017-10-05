---
title: Glossario sugli strumenti di database elastici | Documentazione Microsoft
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
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="b9646-103">Glossario sugli strumenti di database elastici</span><span class="sxs-lookup"><span data-stu-id="b9646-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="b9646-104">Di seguito sono elencate le definizioni dei termini usati per gli [strumenti di database elastici](sql-database-elastic-scale-introduction.md), una funzionalità del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9646-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="b9646-105">Gli strumenti vengono usati per gestire le [mappe partizioni](sql-database-elastic-scale-shard-map-management.md) e includono la [libreria client](sql-database-elastic-database-client-library.md), lo [strumento di suddivisione-unione](sql-database-elastic-scale-overview-split-and-merge.md), i [pool elastici](sql-database-elastic-pool.md) e le [query](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9646-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="b9646-106">Questi termini vengono usati in [Aggiunta di una partizione utilizzando gli strumenti di database elastici](sql-database-elastic-scale-add-a-shard.md) e [Uso della classe RecoveryManager per correggere i problemi delle mappe partizioni](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b9646-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Termini della scalabilità elastica][1]

<span data-ttu-id="b9646-108">**Database**: un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9646-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="b9646-109">**Routing dipendente dei dati**: la funzionalità che consente a un'applicazione di connettersi a una partizione in base a una specifica chiave di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="b9646-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="b9646-110">Vedere [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="b9646-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="b9646-111">Confrontare con **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="b9646-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="b9646-112">**Mappa globale partizioni**: il mapping tra le chiavi di partizionamento orizzontale e le rispettive partizioni all'interno di un **set di partizioni**.</span><span class="sxs-lookup"><span data-stu-id="b9646-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="b9646-113">La mappa partizioni globale viene archiviata nel **gestore mappe partizioni**.</span><span class="sxs-lookup"><span data-stu-id="b9646-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="b9646-114">Confrontare con la **mappa partizioni locale**.</span><span class="sxs-lookup"><span data-stu-id="b9646-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="b9646-115">**Mappa partizioni di tipo elenco**: una mappa partizioni in cui le chiavi di partizionamento orizzontale vengono mappate singolarmente.</span><span class="sxs-lookup"><span data-stu-id="b9646-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="b9646-116">Confrontare con la **mappa partizioni di tipo intervallo**.</span><span class="sxs-lookup"><span data-stu-id="b9646-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="b9646-117">**Mappa partizioni locale**: archiviata in una partizione, la mappa partizioni locale contiene i mapping per gli shardlet che risiedono nella partizione.</span><span class="sxs-lookup"><span data-stu-id="b9646-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="b9646-118">**Esecuzione di query su più partizioni**: la possibilità di eseguire una query su più partizioni; i set di risultati vengono restituiti usando la semantica di UNION ALL (nota anche come "query di tipo fan-out").</span><span class="sxs-lookup"><span data-stu-id="b9646-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="b9646-119">Confrontare con **Routing dipendente dai dati**.</span><span class="sxs-lookup"><span data-stu-id="b9646-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="b9646-120">**Multi-tenant** e **Tenant singolo**: l'immagine mostra un database a tenant singolo e un database multi-tenant:</span><span class="sxs-lookup"><span data-stu-id="b9646-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Database a tenant singolo e multi-tenant](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="b9646-122">Ecco una rappresentazione di database a tenant singolo e multi-tenant **partizionati** .</span><span class="sxs-lookup"><span data-stu-id="b9646-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Database a tenant singolo e multi-tenant](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="b9646-124">**Mappa partizioni di tipo intervallo**: una mappa partizioni in cui la strategia di distribuzione delle partizioni è basata su più intervalli di valori contigui.</span><span class="sxs-lookup"><span data-stu-id="b9646-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="b9646-125">**Tabelle di riferimento**: tabelle che non vengono partizionate, ma vengono replicate tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="b9646-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="b9646-126">I codici di avviamento postale, ad esempio, possono essere archiviati in una tabella di riferimento.</span><span class="sxs-lookup"><span data-stu-id="b9646-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="b9646-127">**Partizione**: un database SQL di Azure che archivia i dati da un set di dati partizionato.</span><span class="sxs-lookup"><span data-stu-id="b9646-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="b9646-128">**Elasticità di partizionamento**: la possibilità di eseguire il **ridimensionamento orizzontale** e il **ridimensionamento verticale**.</span><span class="sxs-lookup"><span data-stu-id="b9646-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="b9646-129">**Tabelle partizionate**: tabelle che vengono partizionate, ovvero i cui dati vengono distribuiti tra le partizioni in base ai valori della chiave di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="b9646-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="b9646-130">**Chiave di partizionamento orizzontale**: un valore di colonna che determina la modalità di distribuzione dei dati tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="b9646-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="b9646-131">Il tipo valore può essere uno dei seguenti: **int**, **bigint**, **varbinary** o **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="b9646-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="b9646-132">**Set di partizioni**: la raccolta di partizioni attribuite alla stessa mappa partizioni nel gestore delle mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="b9646-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="b9646-133">**Shardlet**: il complesso dei dati associati a un singolo valore di una chiave di partizionamento orizzontale in una partizione.</span><span class="sxs-lookup"><span data-stu-id="b9646-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="b9646-134">Uno shardlet è la più piccola unità di spostamento dei dati possibile quando si ridistribuiscono tabelle partizionate.</span><span class="sxs-lookup"><span data-stu-id="b9646-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="b9646-135">**Mappa partizioni**: il set di mapping tra le chiavi di partizionamento orizzontale e le rispettive partizioni.</span><span class="sxs-lookup"><span data-stu-id="b9646-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="b9646-136">**Gestore mappe partizioni**: un archivio di dati e oggetti di gestione che contiene le mappe partizioni, i percorsi delle partizioni e i mapping per uno o più set di partizioni.</span><span class="sxs-lookup"><span data-stu-id="b9646-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mapping][2]

## <a name="verbs"></a><span data-ttu-id="b9646-138">Verbi</span><span class="sxs-lookup"><span data-stu-id="b9646-138">Verbs</span></span>
<span data-ttu-id="b9646-139">**Scalare orizzontalmente**: aumentare o ridurre le dimensioni di una raccolta di partizioni aggiungendo o rimuovendo partizioni a una mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="b9646-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Scalabilità orizzontale e verticale][3]

<span data-ttu-id="b9646-141">**Unire**: spostare shardlet da due partizioni a una partizione e aggiornare la mappa partizioni di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="b9646-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="b9646-142">**Spostare shardlet**: spostare un singolo shardlet in una partizione diversa.</span><span class="sxs-lookup"><span data-stu-id="b9646-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="b9646-143">**Partizione**: eseguire il partizionamento orizzontale di dati strutturati in modo identico in più database in base a una chiave di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="b9646-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="b9646-144">**Dividere**: spostare più shardlet da una partizione a un'altra (in genere nuova).</span><span class="sxs-lookup"><span data-stu-id="b9646-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="b9646-145">Come punto di divisione viene usata una chiave di partizionamento orizzontale fornita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="b9646-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="b9646-146">**Scalare verticalmente**: aumentare o ridurre il livello di prestazioni di una singola partizione.</span><span class="sxs-lookup"><span data-stu-id="b9646-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="b9646-147">Ad esempio, modifica di una partizione da Standard a Premium (che comporta più risorse di elaborazione).</span><span class="sxs-lookup"><span data-stu-id="b9646-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

