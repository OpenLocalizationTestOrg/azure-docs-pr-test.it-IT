---
title: 'T-SQL: gestire un pool elastico di database SQL di Azure | Microsoft Docs'
description: Utilizzare T-SQL toomanage un pool elastico del Database SQL di Azure.
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="6fe6c-103">Monitorare e gestire un pool elastico con Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="6fe6c-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="6fe6c-104">In questo argomento illustra come toomanage scalabile [pool elastici](sql-database-elastic-pool.md) con Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="6fe6c-105">È anche possibile creare e gestire un hello Azure pool elastico [portale di Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello l'API REST o [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6c-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="6fe6c-106">È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6c-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="6fe6c-107">Hello utilizzare [Create Database (Database SQL di Azure)](https://msdn.microsoft.com/library/dn268335.aspx) e [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) comandi toocreate e spostamento di database in e da un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="6fe6c-108">pool elastico Hello deve essere presente prima di poter usare questi comandi.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="6fe6c-109">che hanno effetto solo sui database.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-109">These commands affect only databases.</span></span> <span data-ttu-id="6fe6c-110">Impossibile modificare la creazione di nuovi pool e hello dell'impostazione della proprietà di pool di applicazioni (ad esempio min e max Edtu) con i comandi T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="6fe6c-111">Creare un nuovo database in pool in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="6fe6c-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="6fe6c-112">Comando CREATE DATABASE hello con opzione di SERVICE_OBJECTIVE hello.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="6fe6c-113">Tutti i database in un pool elastico ereditano il livello di servizio hello del pool elastico di hello (Basic, Standard e Premium).</span><span class="sxs-lookup"><span data-stu-id="6fe6c-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="6fe6c-114">Spostare un database tra pool elastici</span><span class="sxs-lookup"><span data-stu-id="6fe6c-114">Move a database between elastic pools</span></span>
<span data-ttu-id="6fe6c-115">Comando ALTER DATABASE hello con hello modifica e impostare servizio\_opzione obiettivo come ELASTICA\_POOL.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="6fe6c-116">Impostare toohello nome hello del pool di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="6fe6c-117">Spostare un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="6fe6c-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="6fe6c-118">Comando ALTER DATABASE hello con hello modifica e impostare servizio\_opzione obiettivo come ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="6fe6c-119">Impostare toohello nome hello del pool di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="6fe6c-120">Spostare un database da un pool elastico</span><span class="sxs-lookup"><span data-stu-id="6fe6c-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="6fe6c-121">Utilizzare il comando di ALTER DATABASE hello e impostare hello SERVICE_OBJECTIVE tooone hello livelli di prestazioni (ad esempio S0 o S1).</span><span class="sxs-lookup"><span data-stu-id="6fe6c-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="6fe6c-122">Elencare i database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="6fe6c-122">List databases in an elastic pool</span></span>
<span data-ttu-id="6fe6c-123">Hello utilizzare [sys\_servizio \_visualizzazione obiettivi](https://msdn.microsoft.com/library/mt712619) toolist tutti hello database in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="6fe6c-124">Visualizzazione del log nel database master toohello database tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="6fe6c-125">Ottenere i dati di utilizzo delle risorse per un pool elastico</span><span class="sxs-lookup"><span data-stu-id="6fe6c-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="6fe6c-126">Hello utilizzare [sys.elastic\_pool \_risorse \_Visualizza statistiche](https://msdn.microsoft.com/library/mt280062.aspx) statistiche di utilizzo delle risorse di tooexamine hello di un pool elastico in un server logico.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="6fe6c-127">Visualizzazione del log nel database master toohello database tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="6fe6c-128">Ottenere l'utilizzo delle risorse per un database in pool</span><span class="sxs-lookup"><span data-stu-id="6fe6c-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="6fe6c-129">Hello utilizzare [sys.dm\_ db\_ risorse\_Visualizza statistiche](https://msdn.microsoft.com/library/dn800981.aspx) o [sys.resource \_Visualizza statistiche](https://msdn.microsoft.com/library/dn269979.aspx) statistiche di utilizzo delle risorse di tooexamine hello di un database in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="6fe6c-130">Questo processo è simile tooquerying utilizzo delle risorse per un singolo database.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fe6c-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6fe6c-131">Next steps</span></span>
<span data-ttu-id="6fe6c-132">Dopo aver creato un pool elastico, è possibile gestire i database elastici nel pool di hello creando processi elastici.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="6fe6c-133">Elastici processi facilitano l'esecuzione di script T-SQL rispetto a qualsiasi numero di database nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="6fe6c-134">Per ulteriori informazioni, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6c-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="6fe6c-135">Vedere [scalabilità orizzontale con Database SQL di Azure](sql-database-elastic-scale-introduction.md): utilizzare tooscale strumenti di database elastico out, spostare i dati, eseguire una query o creare transazioni.</span><span class="sxs-lookup"><span data-stu-id="6fe6c-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

