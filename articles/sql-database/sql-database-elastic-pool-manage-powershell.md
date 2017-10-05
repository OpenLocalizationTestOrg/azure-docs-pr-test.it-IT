---
title: 'PowerShell: creare e gestire un pool elastico SQL di Azure | Microsoft Docs'
description: Informazioni su come usare PowerShell per gestire un pool elastico.
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="b488c-103">Creare e gestire un pool elastico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b488c-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="b488c-104">Questo argomento illustra come creare e gestire [pool elastici](sql-database-elastic-pool.md) scalabili con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b488c-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="b488c-105">È anche possibile creare e gestire un pool elastico di Azure con il [portale di Azure](https://portal.azure.com/), l'API REST o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b488c-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="b488c-106">È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="b488c-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="b488c-107">Creare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-107">Create an elastic pool</span></span>
<span data-ttu-id="b488c-108">Il cmdlet [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) crea un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="b488c-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="b488c-109">I valori per eDTU per pool, DTU min e max sono vincolati dal valore del livello di servizio (Basic, Standard, Premium o Premium RS).</span><span class="sxs-lookup"><span data-stu-id="b488c-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="b488c-110">Vedere [Limiti di archiviazione e di eDTU per pool elastici e database in pool](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="b488c-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="b488c-111">Creare un nuovo database in pool in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="b488c-112">Usare il cmdlet [New- AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) e impostare il parametro **ElasticPoolName** per il pool di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b488c-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="b488c-113">Per spostare un database esistente in un pool elastico, vedere [Spostare un database in un pool elastico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="b488c-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="b488c-114">Script completo</span><span class="sxs-lookup"><span data-stu-id="b488c-114">Complete script</span></span>
<span data-ttu-id="b488c-115">Questo script crea un gruppo di risorse di Azure e un server.</span><span class="sxs-lookup"><span data-stu-id="b488c-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="b488c-116">Quando richiesto, specificare un nome utente dell'amministratore e una password per il nuovo server (non le credenziali di Azure).</span><span class="sxs-lookup"><span data-stu-id="b488c-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="b488c-117">Creare un pool elastico e aggiungere più database in pool</span><span class="sxs-lookup"><span data-stu-id="b488c-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="b488c-118">La creazione di molti database in un pool elastico può richiedere tempo quando viene eseguita tramite il portale o i cmdlet di PowerShell che creano un database singolo alla volta.</span><span class="sxs-lookup"><span data-stu-id="b488c-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="b488c-119">Per automatizzare la creazione in un pool elastico, vedere [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="b488c-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="b488c-120">Spostare un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="b488c-121">È possibile spostare un database all'interno o all'esterno di un pool elastico con [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="b488c-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="b488c-122">Modificare le impostazioni delle prestazioni di un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="b488c-123">Quando le prestazioni ne risentono, è possibile modificare le impostazioni del pool per supportare la crescita.</span><span class="sxs-lookup"><span data-stu-id="b488c-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="b488c-124">Usare il cmdlet [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="b488c-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="b488c-125">Impostare il parametro -Dtu sul numero di eDTU per pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="b488c-126">Per i valori possibili, vedere [Limiti di archiviazione e di eDTU dei pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="b488c-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="b488c-127">Modificare il limite di archiviazione per un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="b488c-128">Usare il cmdlet [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) per impostare il parametro _-StorageMB_.</span><span class="sxs-lookup"><span data-stu-id="b488c-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="b488c-129">Specificare il limite di archiviazione in MB. Con 2097152, ad esempio, il limite di archiviazione viene impostato su 2 TB.</span><span class="sxs-lookup"><span data-stu-id="b488c-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="b488c-130">Per i valori possibili, vedere [Limiti di archiviazione e di eDTU dei pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="b488c-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b488c-131">Lo spazio di archiviazione dati massimo predefinito per pool Premium con 1500 o più eDTU è 750 GB.</span><span class="sxs-lookup"><span data-stu-id="b488c-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="b488c-132">Per ottenere _dimensioni di archiviazione dati massime per pool_ superiori, è necessario impostare il limite di archiviazione in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="b488c-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="b488c-133">I pool Premium con spazio di archiviazione superiore a 750 GB sono attualmente in anteprima pubblica nelle aree seguenti: Stati Uniti orientali 2, Stati Uniti occidentali, US Gov Virginia, Europa occidentale, Germania centrale, Asia sud-orientale, Giappone orientale, Australia orientale, Canada centrale e Canada orientale.</span><span class="sxs-lookup"><span data-stu-id="b488c-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="b488c-134">Ottenere lo stato delle operazioni dei pool</span><span class="sxs-lookup"><span data-stu-id="b488c-134">Get the status of pool operations</span></span>
<span data-ttu-id="b488c-135">La creazione di un pool elastico può richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="b488c-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="b488c-136">Per tenere traccia dello stato delle operazioni dei pool, inclusi la creazione e gli aggiornamenti, usare il cmdlet [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity).</span><span class="sxs-lookup"><span data-stu-id="b488c-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="b488c-137">Ottenere lo stato dello spostamento di un database all'interno o all'esterno di un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="b488c-138">Lo spostamento di un database può richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="b488c-138">Moving a database can take time.</span></span> <span data-ttu-id="b488c-139">Tenere traccia di un stato di spostamento mediante il cmdlet [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity).</span><span class="sxs-lookup"><span data-stu-id="b488c-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="b488c-140">Ottenere i dati di utilizzo delle risorse per un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="b488c-141">Metriche che è possibile recuperare come percentuale del limite del pool di risorse:</span><span class="sxs-lookup"><span data-stu-id="b488c-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="b488c-142">Nome metrica</span><span class="sxs-lookup"><span data-stu-id="b488c-142">Metric name</span></span> | <span data-ttu-id="b488c-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b488c-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b488c-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="b488c-144">cpu\_percent</span></span> |<span data-ttu-id="b488c-145">Utilizzo medio del calcolo espresso in percentuale del limite del pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="b488c-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="b488c-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="b488c-147">Utilizzo I/O medio espresso in percentuale sulla base del limite del pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="b488c-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="b488c-148">log\_write\_percent</span></span> |<span data-ttu-id="b488c-149">Utilizzo delle risorse di scrittura medio espresso in percentuale del limite del pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="b488c-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="b488c-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="b488c-151">Utilizzo di eDTU medio espresso in percentuale del limite di eDTU per pool</span><span class="sxs-lookup"><span data-stu-id="b488c-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="b488c-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="b488c-152">storage\_percent</span></span> |<span data-ttu-id="b488c-153">Utilizzo di spazio di archiviazione medio espresso in percentuale del limite di archiviazione del pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="b488c-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="b488c-154">workers\_percent</span></span> |<span data-ttu-id="b488c-155">Numero massimo di ruoli di lavoro simultanei (richieste) espresso in percentuale sulla base del limite del pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="b488c-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="b488c-156">sessions\_percent</span></span> |<span data-ttu-id="b488c-157">Numero massimo di sessioni simultanee espresso in percentuale sulla base del limite del pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="b488c-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="b488c-158">eDTU_limit</span></span> |<span data-ttu-id="b488c-159">Impostazione del numero massimo DTU del pool elastico corrente per questo pool elastico durante l'intervallo.</span><span class="sxs-lookup"><span data-stu-id="b488c-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="b488c-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="b488c-160">storage\_limit</span></span> |<span data-ttu-id="b488c-161">Impostazione del limite massimo di archiviazione del pool elastico corrente per questo pool elastico espresso in megabyte durante l'intervallo.</span><span class="sxs-lookup"><span data-stu-id="b488c-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="b488c-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="b488c-162">eDTU\_used</span></span> |<span data-ttu-id="b488c-163">Numero medio di eDTU usato dal pool nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="b488c-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="b488c-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="b488c-164">storage\_used</span></span> |<span data-ttu-id="b488c-165">Spazio medio di archiviazione usato dal pool nell'intervallo espresso in byte</span><span class="sxs-lookup"><span data-stu-id="b488c-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="b488c-166">**Granularità della metrica/periodi di conservazione:**</span><span class="sxs-lookup"><span data-stu-id="b488c-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="b488c-167">I dati vengono restituiti con una granularità di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="b488c-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="b488c-168">La conservazione dei dati è di 35 giorni.</span><span class="sxs-lookup"><span data-stu-id="b488c-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="b488c-169">Questo cmdlet e questa API limitano il numero di righe che è possibile recuperare in una chiamata a 1000 righe, ovvero circa 3 giorni di dati con una granularità di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="b488c-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="b488c-170">Tuttavia, questo comando può essere chiamato più volte con intervalli di tempo iniziale e finale differenti per recuperare ulteriori dati</span><span class="sxs-lookup"><span data-stu-id="b488c-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="b488c-171">Per recuperare le metriche:</span><span class="sxs-lookup"><span data-stu-id="b488c-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="b488c-172">Ottenere i dati di utilizzo delle risorse per un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="b488c-173">Queste API sono le stesse API usate per monitorare l'utilizzo delle risorse di un database singolo, tranne per la differenza semantica seguente: le metriche recuperate sono espresse in percentuale del numero massimo di eDTU per database (o di un limite equivalente per la metrica sottostante, ad esempio CPU o I/O) impostato per il pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="b488c-174">Ad esempio, l'utilizzo del 50% di una di queste metriche indica che il consumo di risorse specifico si trova al 50% del limite di utilizzo per database per quella risorsa nel pool padre.</span><span class="sxs-lookup"><span data-stu-id="b488c-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="b488c-175">Per recuperare le metriche:</span><span class="sxs-lookup"><span data-stu-id="b488c-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="b488c-176">Aggiungere un avviso a una risorsa di pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="b488c-177">È possibile aggiungere regole di avviso a un pool elastico per l'invio di notifiche tramite posta elettronica oppure stringhe di avviso a [endpoint di URL](https://msdn.microsoft.com/library/mt718036.aspx) quando il pool elastico raggiunge la soglia di utilizzo impostata.</span><span class="sxs-lookup"><span data-stu-id="b488c-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="b488c-178">Usare il cmdlet Add-AzureRmMetricAlertRule.</span><span class="sxs-lookup"><span data-stu-id="b488c-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b488c-179">Il monitoraggio dell'uso delle risorse per i pool elastici viene eseguito con un ritardo di almeno 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="b488c-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="b488c-180">Al momento non è possibile impostare avvisi inferiori ai 10 minuti per i pool elastici.</span><span class="sxs-lookup"><span data-stu-id="b488c-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="b488c-181">Eventuali avvisi impostato per il pool elastico con un punto (parametro denominato "-WindowSize" nell'API di PowerShell) di meno di 10 minuti non può essere avviata.</span><span class="sxs-lookup"><span data-stu-id="b488c-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="b488c-182">Verificare che gli avvisi definiti per i pool elastici usino un periodo (WindowSize) di almeno 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="b488c-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="b488c-183">In questo esempio viene aggiunto un avviso per ricevere una notifica quando il consumo di eDTU del pool elastico supera una soglia stabilita.</span><span class="sxs-lookup"><span data-stu-id="b488c-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="b488c-184">Per altre informazioni, vedere [Usare il portale di Azure per creare avvisi per il database SQL di Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b488c-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="b488c-185">Aggiungere avvisi a tutti i database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="b488c-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="b488c-186">È possibile aggiungere regole di avviso a tutti i database di un pool elastico in modo che vengano inviate notifiche tramite posta elettronica o stringhe di avviso a [endpoint di URL](https://msdn.microsoft.com/library/mt718036.aspx) quando una risorsa raggiunge la soglia di utilizzo impostata.</span><span class="sxs-lookup"><span data-stu-id="b488c-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b488c-187">Il monitoraggio dell'uso delle risorse per i pool elastici viene eseguito con un ritardo di almeno 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="b488c-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="b488c-188">Al momento non è possibile impostare avvisi inferiori ai 10 minuti per i pool elastici.</span><span class="sxs-lookup"><span data-stu-id="b488c-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="b488c-189">Eventuali avvisi impostato per il pool elastico con un punto (parametro denominato "-WindowSize" nell'API di PowerShell) di meno di 10 minuti non può essere avviata.</span><span class="sxs-lookup"><span data-stu-id="b488c-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="b488c-190">Verificare che gli avvisi definiti per i pool elastici usino un periodo (WindowSize) di almeno 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="b488c-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="b488c-191">Questo esempio aggiunge un avviso a ognuno dei database di un pool elastico in modo che venga inviata una notifica quando il consumo di DTU del database supera una determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="b488c-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="b488c-192">Raccogliere e monitorare i dati sull'utilizzo delle risorse in più pool in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="b488c-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="b488c-193">In presenza di molti database in una sottoscrizione, è difficile monitorare separatamente i singoli pool elastici.</span><span class="sxs-lookup"><span data-stu-id="b488c-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="b488c-194">I cmdlet di PowerShell per database SQL e le query T-SQL, invece, possono essere combinati per raccogliere dati sull'utilizzo delle risorse da più pool e i relativi database per il monitoraggio e l'analisi dell'utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="b488c-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="b488c-195">Nel repository di esempi relativi a SQL Server su GitHub è disponibile un' [implementazione di esempio](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) di un set di script di PowerShell di questo tipo, insieme alla documentazione relativa alle operazioni eseguite da tale implementazione e al relativo uso.</span><span class="sxs-lookup"><span data-stu-id="b488c-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="b488c-196">Per usare questa implementazione di esempio, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="b488c-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="b488c-197">Scaricare gli [script e la documentazione](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="b488c-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="b488c-198">Modificare gli script per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="b488c-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="b488c-199">Specificare uno o più server in cui sono ospitati i pool elastici.</span><span class="sxs-lookup"><span data-stu-id="b488c-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="b488c-200">Specificare un database di telemetria in cui archiviare le metriche raccolte.</span><span class="sxs-lookup"><span data-stu-id="b488c-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="b488c-201">Personalizzare lo script per specificare la durata dell'esecuzione degli script.</span><span class="sxs-lookup"><span data-stu-id="b488c-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="b488c-202">A livello generale, gli script eseguono le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b488c-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="b488c-203">Enumera tutti i server in una determinata sottoscrizione di Azure (o in determinato elenco di server).</span><span class="sxs-lookup"><span data-stu-id="b488c-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="b488c-204">Esegue un processo in background per ogni server.</span><span class="sxs-lookup"><span data-stu-id="b488c-204">Runs a background job for each server.</span></span> <span data-ttu-id="b488c-205">Il processo viene eseguito in un ciclo a intervalli regolari e raccoglie i dati di telemetria per tutti i pool nel server.</span><span class="sxs-lookup"><span data-stu-id="b488c-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="b488c-206">Carica quindi i dati raccolti nel database di telemetria specificato.</span><span class="sxs-lookup"><span data-stu-id="b488c-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="b488c-207">Enumera un elenco di database in ogni pool per raccogliere i dati sull'utilizzo delle risorse di database.</span><span class="sxs-lookup"><span data-stu-id="b488c-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="b488c-208">Carica quindi i dati raccolti nel database di telemetria.</span><span class="sxs-lookup"><span data-stu-id="b488c-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="b488c-209">È possibile analizzare le metriche raccolte nel database di telemetria per monitorare l'integrità dei pool elastici e i database che contengono.</span><span class="sxs-lookup"><span data-stu-id="b488c-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="b488c-210">Lo script installa anche una funzione con valori di tabella predefinita nel database di telemetria per aggregare le metriche per un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="b488c-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="b488c-211">Ad esempio, i risultati della funzione con valori di tabella possono essere usati per visualizzare i "primi N pool elastici con l'utilizzo eDTU massimo in un dato intervallo di tempo".</span><span class="sxs-lookup"><span data-stu-id="b488c-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="b488c-212">Facoltativamente, è possibile usare strumenti di analisi come Excel o Power BI per eseguire una query e analizzare i dati raccolti.</span><span class="sxs-lookup"><span data-stu-id="b488c-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="b488c-213">Esempio: recuperare le metriche di consumo di risorse per un pool elastico e i relativi database</span><span class="sxs-lookup"><span data-stu-id="b488c-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="b488c-214">Questo esempio recupera le metriche di consumo per un determinato pool elastico e tutti i relativi database.</span><span class="sxs-lookup"><span data-stu-id="b488c-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="b488c-215">I dati raccolti vengono formattati e scritti in un file in formato CSV.</span><span class="sxs-lookup"><span data-stu-id="b488c-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="b488c-216">Il file può essere esplorato in Excel.</span><span class="sxs-lookup"><span data-stu-id="b488c-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="b488c-217">Latenza delle operazioni dei pool elastici</span><span class="sxs-lookup"><span data-stu-id="b488c-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="b488c-218">La modifica del numero minimo di eDTU per database o del numero massimo di eDTU per database in genere viene completata entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="b488c-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="b488c-219">La modifica del numero di eDTU per pool dipende dallo spazio totale usato da tutti i database nel pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="b488c-220">Le modifiche richiedono una media di 90 minuti o meno per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="b488c-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="b488c-221">Ad esempio, se lo spazio totale utilizzato da tutti i database nel pool è pari a 200 GB, la latenza prevista per la modifica del numero di eDTU del pool per ogni pool è di 3 ore o meno.</span><span class="sxs-lookup"><span data-stu-id="b488c-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b488c-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b488c-222">Next steps</span></span>
* <span data-ttu-id="b488c-223">[Creare processi elastici](sql-database-elastic-jobs-overview.md) : i processi elastici consentono di eseguire script T-SQL su un numero qualsiasi di database nel pool.</span><span class="sxs-lookup"><span data-stu-id="b488c-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="b488c-224">Vedere [Aumentare il numero di istanze con il database SQL di Azure](sql-database-elastic-scale-introduction.md): usare gli strumenti elastici per aumentare il numero di istanze, spostare dati, eseguire query o creare transazioni.</span><span class="sxs-lookup"><span data-stu-id="b488c-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
