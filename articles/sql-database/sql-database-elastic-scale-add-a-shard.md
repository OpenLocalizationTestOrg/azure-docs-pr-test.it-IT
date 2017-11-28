---
title: aaaAdding una partizione utilizzando gli strumenti di database elastico | Documenti Microsoft
description: "Come imposta toouse API di scalabilità elastica tooadd nuova partizioni tooa partizione."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="a6974-103">Aggiunta di una partizione utilizzando gli strumenti di database elastici</span><span class="sxs-lookup"><span data-stu-id="a6974-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="a6974-104">tooadd una partizione per un nuovo intervallo o una chiave</span><span class="sxs-lookup"><span data-stu-id="a6974-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="a6974-105">Le applicazioni spesso necessario toosimply aggiungere nuovi dati toohandle partizioni che si prevedono di nuove chiavi o intervalli di chiavi per una mappa partizioni è già esistente.</span><span class="sxs-lookup"><span data-stu-id="a6974-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="a6974-106">Ad esempio, un'applicazione partizionata in base l'ID Tenant potrebbe essere necessario tooprovision una nuova partizione per un nuovo tenant o mensile partizionati dati potrebbe essere una nuova partizione provisioning prima dell'inizio hello di ogni nuovo mese.</span><span class="sxs-lookup"><span data-stu-id="a6974-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="a6974-107">Se il nuovo intervallo di valori di chiave di hello non fa già parte di un mapping esistente, è molto semplice tooadd hello nuova partizione e associare hello nuova chiave o un intervallo toothat partizione.</span><span class="sxs-lookup"><span data-stu-id="a6974-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="a6974-108">Esempio: aggiunta di una partizione e la mappa di partizione esistente intervallo tooan</span><span class="sxs-lookup"><span data-stu-id="a6974-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="a6974-109">In questo esempio utilizza hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) metodi e crea un'istanza di hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe.</span><span class="sxs-lookup"><span data-stu-id="a6974-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="a6974-110">Esempio hello riportato di seguito, un database denominato **sample_shard_2** e tutti gli oggetti necessarie per lo schema in essa sono stati creati toohold intervallo [300, 400).</span><span class="sxs-lookup"><span data-stu-id="a6974-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="a6974-111">In alternativa, è possibile utilizzare Powershell toocreate un nuovo gestore mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="a6974-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="a6974-112">Un esempio è disponibile [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="a6974-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="a6974-113">tooadd una partizione per una parte vuota di un intervallo esistente</span><span class="sxs-lookup"><span data-stu-id="a6974-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="a6974-114">In alcuni casi, si possono avere già eseguito il mapping di una partizione tooa intervallo e parzialmente viene riempita con i dati, ma ora è diverse partizioni di dati futuri toobe tooa diretto.</span><span class="sxs-lookup"><span data-stu-id="a6974-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="a6974-115">Ad esempio, si partizioni dal giorno intervallo e hanno già allocato partizione tooa 50 giorni, ma giorno 24, si desidera che i dati futuri tooland in una partizione diversa.</span><span class="sxs-lookup"><span data-stu-id="a6974-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="a6974-116">database elastico Hello [strumento di merge di divisione](sql-database-elastic-scale-overview-split-and-merge.md) possono eseguire questa operazione, ma se lo spostamento dei dati non è necessario (ad esempio dati per intervallo hello di giorni [25, 50), ad esempio, giorno 25 inclusivo too50 esclusivo, non esiste ancora) è possibile eseguire Questo utilizzo completamente hello direttamente le API di gestione di partizioni della mappa.</span><span class="sxs-lookup"><span data-stu-id="a6974-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="a6974-117">Esempio: suddivisione di un intervallo e l'assegnazione di hello vuote partizione appena aggiunti tooa di parte</span><span class="sxs-lookup"><span data-stu-id="a6974-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="a6974-118">È stato creato un database denominato "sample_shard_2" contenente tutti gli oggetti di schema necessari.</span><span class="sxs-lookup"><span data-stu-id="a6974-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="a6974-119">**Importante**: utilizzare questa tecnica solo se si è certi che hello intervallo per il mapping di hello aggiornato è vuoto.</span><span class="sxs-lookup"><span data-stu-id="a6974-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="a6974-120">dati per intervallo hello spostato non controllati da metodi Hello precedenti, è preferibile tooinclude verifica nel codice.</span><span class="sxs-lookup"><span data-stu-id="a6974-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="a6974-121">Se sono presenti righe nell'intervallo di hello viene spostato, distribuzione di dati effettivi hello non corrisponderanno mappa partizioni aggiornato hello.</span><span class="sxs-lookup"><span data-stu-id="a6974-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="a6974-122">Hello utilizzare [strumento di merge di divisione](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello invece l'operazione in questi casi.</span><span class="sxs-lookup"><span data-stu-id="a6974-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

