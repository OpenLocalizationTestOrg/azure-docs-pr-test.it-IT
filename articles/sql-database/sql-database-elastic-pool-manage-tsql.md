---
title: 'T-SQL: gestire un pool elastico di database SQL di Azure | Microsoft Docs'
description: Usare T-SQL per gestire un pool elastico di database SQL di Azure.
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
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="b20db-103">Monitorare e gestire un pool elastico con Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="b20db-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="b20db-104">Questo argomento illustra come gestire [pool elastici](sql-database-elastic-pool.md) scalabili con Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="b20db-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="b20db-105">È anche possibile creare e gestire un pool elastico di Azure con il [portale di Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), l'API REST o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b20db-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="b20db-106">È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="b20db-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="b20db-107">Usare i comandi [Create Database (database SQL di Azure)](https://msdn.microsoft.com/library/dn268335.aspx) e [Alter Database (database SQL di Azure)](https://msdn.microsoft.com/library/mt574871.aspx) per creare e spostare i database all'interno e all'esterno di pool elastici.</span><span class="sxs-lookup"><span data-stu-id="b20db-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="b20db-108">Il pool elastico deve essere già disponibile per poter usare questi comandi,</span><span class="sxs-lookup"><span data-stu-id="b20db-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="b20db-109">che hanno effetto solo sui database.</span><span class="sxs-lookup"><span data-stu-id="b20db-109">These commands affect only databases.</span></span> <span data-ttu-id="b20db-110">La creazione di nuovi pool e l'impostazione delle proprietà dei pool, ad esempio eDTU min/max, non possono essere modificate con i comandi T-SQL.</span><span class="sxs-lookup"><span data-stu-id="b20db-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="b20db-111">Creare un nuovo database in pool in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b20db-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="b20db-112">Usare il comando CREATE DATABASE con l'opzione SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="b20db-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="b20db-113">Tutti i database in un pool elastico ereditano il livello di servizio del pool elastico (Basic, Standard o Premium).</span><span class="sxs-lookup"><span data-stu-id="b20db-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="b20db-114">Spostare un database tra pool elastici</span><span class="sxs-lookup"><span data-stu-id="b20db-114">Move a database between elastic pools</span></span>
<span data-ttu-id="b20db-115">Usare il comando ALTER DATABASE con MODIFY e impostare l'opzione SERVICE\_OBJECTIVE come ELASTIC\_POOL.</span><span class="sxs-lookup"><span data-stu-id="b20db-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="b20db-116">Come nome, impostare il nome del pool di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b20db-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="b20db-117">Spostare un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b20db-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="b20db-118">Usare il comando ALTER DATABASE con MODIFY e impostare l'opzione SERVICE\_OBJECTIVE come ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="b20db-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="b20db-119">Come nome, impostare il nome del pool di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b20db-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="b20db-120">Spostare un database da un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b20db-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="b20db-121">Usare il comando ALTER DATABASE e impostare SERVICE_OBJECTIVE su uno dei livelli di prestazioni, ad esempio S0 o S1.</span><span class="sxs-lookup"><span data-stu-id="b20db-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="b20db-122">Elencare i database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b20db-122">List databases in an elastic pool</span></span>
<span data-ttu-id="b20db-123">Usare la [vista sys.database\_service \_objectives](https://msdn.microsoft.com/library/mt712619) per elencare tutti i database in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="b20db-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="b20db-124">Accedere al database master per eseguire query sulla vista.</span><span class="sxs-lookup"><span data-stu-id="b20db-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="b20db-125">Ottenere i dati di utilizzo delle risorse per un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b20db-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="b20db-126">Usare la [vista sys.elastic\_pool \_resource \_stats](https://msdn.microsoft.com/library/mt280062.aspx) per esaminare le statistiche di utilizzo delle risorse di un pool elastico in un server logico.</span><span class="sxs-lookup"><span data-stu-id="b20db-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="b20db-127">Accedere al database master per eseguire query sulla vista.</span><span class="sxs-lookup"><span data-stu-id="b20db-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="b20db-128">Ottenere l'utilizzo delle risorse per un database in pool</span><span class="sxs-lookup"><span data-stu-id="b20db-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="b20db-129">Usare la [vista sys.dm\_db\_ resource\_stats](https://msdn.microsoft.com/library/dn800981.aspx) o la [vista sys.resource\_stats](https://msdn.microsoft.com/library/dn269979.aspx) per esaminare le statistiche di utilizzo delle risorse di un database in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="b20db-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="b20db-130">Questo processo è simile all'esecuzione di query sull'utilizzo delle risorse per un database singolo.</span><span class="sxs-lookup"><span data-stu-id="b20db-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b20db-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b20db-131">Next steps</span></span>
<span data-ttu-id="b20db-132">Dopo aver creato un pool elastico, è possibile gestire i database elastici nel pool mediante la creazione di processi elastici.</span><span class="sxs-lookup"><span data-stu-id="b20db-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="b20db-133">I processi elastici facilitano l’esecuzione di script T-SQL su qualsiasi numero di database nel pool.</span><span class="sxs-lookup"><span data-stu-id="b20db-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="b20db-134">Per ulteriori informazioni, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b20db-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="b20db-135">Vedere [Aumentare il numero di istanze con il database SQL di Azure](sql-database-elastic-scale-introduction.md): usare gli strumenti di database elastici per aumentare il numero di istanze, spostare dati, eseguire query o creare transazioni.</span><span class="sxs-lookup"><span data-stu-id="b20db-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

