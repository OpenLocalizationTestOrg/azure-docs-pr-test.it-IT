---
title: 'PowerShell: creare e gestire un pool elastico SQL di Azure | Microsoft Docs'
description: Informazioni su come toouse PowerShell toomanage un pool elastico.
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
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="cebd7-103">Creare e gestire un pool elastico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="cebd7-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="cebd7-104">In questo argomento illustra come toocreate e gestire scalabile [pool elastici](sql-database-elastic-pool.md) con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cebd7-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="cebd7-105">È anche possibile creare e gestire un pool elastico Azure utilizzando hello [portale di Azure](https://portal.azure.com/), l'API REST o [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="cebd7-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="cebd7-106">È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="cebd7-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="cebd7-107">Creare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-107">Create an elastic pool</span></span>
<span data-ttu-id="cebd7-108">Hello [New AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet crea un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="cebd7-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="cebd7-109">i valori Hello per eDTU per pool e min Dtu massime sono vincolati dal valore del livello servizio hello (Basic, Standard, Premium o RS Premium).</span><span class="sxs-lookup"><span data-stu-id="cebd7-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="cebd7-110">Vedere [Limiti di archiviazione e di eDTU per pool elastici e database in pool](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="cebd7-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="cebd7-111">Creare un nuovo database in pool in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="cebd7-112">Hello utilizzare [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet e set hello **ElasticPoolName** pool di destinazione toohello di parametro.</span><span class="sxs-lookup"><span data-stu-id="cebd7-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="cebd7-113">toomove un database esistente in un pool elastico, vedere [spostare un database in un pool elastico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="cebd7-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="cebd7-114">Script completo</span><span class="sxs-lookup"><span data-stu-id="cebd7-114">Complete script</span></span>
<span data-ttu-id="cebd7-115">Questo script crea un gruppo di risorse di Azure e un server.</span><span class="sxs-lookup"><span data-stu-id="cebd7-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="cebd7-116">Quando richiesto, fornire un nome utente amministratore e una password per nuovo server di hello (non le credenziali di Azure).</span><span class="sxs-lookup"><span data-stu-id="cebd7-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="cebd7-117">Creare un pool elastico e aggiungere più database in pool</span><span class="sxs-lookup"><span data-stu-id="cebd7-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="cebd7-118">Creazione di molti database in un pool elastico può richiedere tempo al termine della hello portale o i cmdlet di PowerShell che creano solo un singolo database alla volta.</span><span class="sxs-lookup"><span data-stu-id="cebd7-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="cebd7-119">creazione di tooautomate in un pool elastico, vedere [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="cebd7-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="cebd7-120">Spostare un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="cebd7-121">È possibile spostare un database interno o all'esterno di un pool elastico con hello [Set AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="cebd7-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="cebd7-122">Modificare le impostazioni delle prestazioni di un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="cebd7-123">Quando le prestazioni risultano lente, è possibile modificare impostazioni hello di crescita di hello pool tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="cebd7-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="cebd7-124">Hello utilizzare [Set AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cebd7-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="cebd7-125">Impostare hello - Dtu parametro toohello Edtu per pool.</span><span class="sxs-lookup"><span data-stu-id="cebd7-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="cebd7-126">Per i valori possibili, vedere [Limiti di archiviazione e di eDTU dei pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="cebd7-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="cebd7-127">Modificare il limite di archiviazione hello per un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="cebd7-128">Hello utilizzare [Set AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _- StorageMB_ parametro.</span><span class="sxs-lookup"><span data-stu-id="cebd7-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="cebd7-129">Specificare il limite di archiviazione hello in MB (ad esempio, 2097152 imposta hello archiviazione limite too2 TB).</span><span class="sxs-lookup"><span data-stu-id="cebd7-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="cebd7-130">Per i valori possibili, vedere [Limiti di archiviazione e di eDTU dei pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="cebd7-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cebd7-131">archiviazione di dati max Hello predefinita per ogni pool per pool Premium con 1500 Edtu o più sono 750 GB.</span><span class="sxs-lookup"><span data-stu-id="cebd7-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="cebd7-132">hello tooobtain superiore _max dimensioni di archiviazione di dati per ogni pool_, il limite di archiviazione hello deve essere impostato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="cebd7-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="cebd7-133">Pool Premium con più di 750 GB di spazio di archiviazione è attualmente in anteprima pubblica di hello seguenti aree: Stati Uniti orientali 2, Stati Uniti occidentali, ci Gov Virginia, Europa occidentale, Germania centrale, Asia sudorientale, Giappone orientale, Australia orientale, Canada centrale e in Canada orientale.</span><span class="sxs-lookup"><span data-stu-id="cebd7-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="cebd7-134">Ottenere lo stato di hello delle operazioni del pool</span><span class="sxs-lookup"><span data-stu-id="cebd7-134">Get hello status of pool operations</span></span>
<span data-ttu-id="cebd7-135">La creazione di un pool elastico può richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="cebd7-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="cebd7-136">stato hello tootrack delle operazioni del pool inclusi la creazione e gli aggiornamenti, utilizzare hello [Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cebd7-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="cebd7-137">Ottenere lo stato di hello di spostamento di un database in e da un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="cebd7-138">Lo spostamento di un database può richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="cebd7-138">Moving a database can take time.</span></span> <span data-ttu-id="cebd7-139">Tenere traccia di uno stato di spostamento tramite hello [Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cebd7-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="cebd7-140">Ottenere i dati di utilizzo delle risorse per un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="cebd7-141">Metriche che possono essere recuperate come percentuale del limite di pool di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="cebd7-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="cebd7-142">Nome metrica</span><span class="sxs-lookup"><span data-stu-id="cebd7-142">Metric name</span></span> | <span data-ttu-id="cebd7-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cebd7-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cebd7-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="cebd7-144">cpu\_percent</span></span> |<span data-ttu-id="cebd7-145">Utilizzo di calcolo Media in percentuale del limite di hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="cebd7-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="cebd7-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="cebd7-147">Utilizzo medio dei / o in percentuale hello limite del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="cebd7-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="cebd7-148">log\_write\_percent</span></span> |<span data-ttu-id="cebd7-149">Medio scrittura utilizzo delle risorse in percentuale del limite di hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="cebd7-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="cebd7-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="cebd7-151">Utilizzo di eDTU medio espresso come percentuale del limite di eDTU per pool hello</span><span class="sxs-lookup"><span data-stu-id="cebd7-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="cebd7-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="cebd7-152">storage\_percent</span></span> |<span data-ttu-id="cebd7-153">Utilizzo di spazio di archiviazione medio espresso come percentuale del limite di archiviazione hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="cebd7-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="cebd7-154">workers\_percent</span></span> |<span data-ttu-id="cebd7-155">Massimi simultanee processi di lavoro (richieste), espresso in percentuale basata sul limite di hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="cebd7-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="cebd7-156">sessions\_percent</span></span> |<span data-ttu-id="cebd7-157">Numero massimo di sessioni simultaneo espresso come percentuale sul limite di hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="cebd7-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="cebd7-158">eDTU_limit</span></span> |<span data-ttu-id="cebd7-159">Impostazione del numero massimo DTU del pool elastico corrente per questo pool elastico durante l'intervallo.</span><span class="sxs-lookup"><span data-stu-id="cebd7-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="cebd7-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="cebd7-160">storage\_limit</span></span> |<span data-ttu-id="cebd7-161">Impostazione del limite massimo di archiviazione del pool elastico corrente per questo pool elastico espresso in megabyte durante l'intervallo.</span><span class="sxs-lookup"><span data-stu-id="cebd7-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="cebd7-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="cebd7-162">eDTU\_used</span></span> |<span data-ttu-id="cebd7-163">Numero di Edtu Media utilizzata dal pool hello in questo intervallo.</span><span class="sxs-lookup"><span data-stu-id="cebd7-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="cebd7-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="cebd7-164">storage\_used</span></span> |<span data-ttu-id="cebd7-165">Spazio di archiviazione medio utilizzato dal pool hello in questo intervallo, in byte</span><span class="sxs-lookup"><span data-stu-id="cebd7-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="cebd7-166">**Granularità della metrica/periodi di conservazione:**</span><span class="sxs-lookup"><span data-stu-id="cebd7-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="cebd7-167">I dati vengono restituiti con una granularità di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="cebd7-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="cebd7-168">La conservazione dei dati è di 35 giorni.</span><span class="sxs-lookup"><span data-stu-id="cebd7-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="cebd7-169">Questa API e i cmdlet limita il numero di hello di righe che possono essere recuperati in un'unica chiamata too1000 righe (circa 3 giorni di dati con granularità di 5 minuti).</span><span class="sxs-lookup"><span data-stu-id="cebd7-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="cebd7-170">Ma questo comando può essere chiamato più volte con tooretrieve intervalli di tempo iniziale o finale di diversi altri dati</span><span class="sxs-lookup"><span data-stu-id="cebd7-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="cebd7-171">metrica di hello tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="cebd7-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="cebd7-172">Ottenere i dati di utilizzo delle risorse per un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="cebd7-173">Queste API sono hello stesso hello API utilizzate per il monitoraggio di utilizzo delle risorse di un singolo database, ad eccezione delle seguenti differenze semantiche hello hello: le metriche recuperate sono espresse come percentuale di hello per ogni database max Edtu (o equivalente cap per hello sottostante metrica come CPU o dei / o) impostato per tale pool.</span><span class="sxs-lookup"><span data-stu-id="cebd7-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="cebd7-174">50% di utilizzo di uno qualsiasi di queste metriche, ad esempio, indica che il consumo di risorse specifico hello al 50% di hello al limite di database per tale risorsa nel pool di hello padre.</span><span class="sxs-lookup"><span data-stu-id="cebd7-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="cebd7-175">metrica di hello tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="cebd7-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="cebd7-176">Aggiungere una risorsa del pool elastico tooan avviso</span><span class="sxs-lookup"><span data-stu-id="cebd7-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="cebd7-177">È possibile aggiungere regole di avviso tooan pool elastico toosend notifiche tramite posta elettronica o l'avviso stringhe troppo[endpoint URL](https://msdn.microsoft.com/library/mt718036.aspx) quando pool elastico hello raggiunga una soglia di utilizzo impostato.</span><span class="sxs-lookup"><span data-stu-id="cebd7-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="cebd7-178">Utilizzare il cmdlet Add-AzureRmMetricAlertRule hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cebd7-179">Il monitoraggio dell'uso delle risorse per i pool elastici viene eseguito con un ritardo di almeno 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="cebd7-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="cebd7-180">Al momento non è possibile impostare avvisi inferiori ai 10 minuti per i pool elastici.</span><span class="sxs-lookup"><span data-stu-id="cebd7-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="cebd7-181">Eventuali avvisi impostato per il pool elastico con un punto (parametro denominato "-WindowSize" nell'API di PowerShell) di meno di 10 minuti non può essere avviata.</span><span class="sxs-lookup"><span data-stu-id="cebd7-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="cebd7-182">Verificare che gli avvisi definiti per i pool elastici usino un periodo (WindowSize) di almeno 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="cebd7-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="cebd7-183">In questo esempio viene aggiunto un avviso per ricevere una notifica quando il consumo di eDTU del pool elastico supera una soglia stabilita.</span><span class="sxs-lookup"><span data-stu-id="cebd7-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="cebd7-184">Per altre informazioni, vedere [Usare il portale di Azure per creare avvisi per il database SQL di Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cebd7-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="cebd7-185">Aggiungere database tooall degli avvisi in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="cebd7-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="cebd7-186">È possibile aggiungere regole di avviso database tooall in un pool elastico di toosend notifiche tramite posta elettronica o l'avviso stringhe troppo[endpoint URL](https://msdn.microsoft.com/library/mt718036.aspx) quando una risorsa raggiunga una soglia di utilizzo impostata dall'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cebd7-187">Il monitoraggio dell'uso delle risorse per i pool elastici viene eseguito con un ritardo di almeno 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="cebd7-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="cebd7-188">Al momento non è possibile impostare avvisi inferiori ai 10 minuti per i pool elastici.</span><span class="sxs-lookup"><span data-stu-id="cebd7-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="cebd7-189">Eventuali avvisi impostato per il pool elastico con un punto (parametro denominato "-WindowSize" nell'API di PowerShell) di meno di 10 minuti non può essere avviata.</span><span class="sxs-lookup"><span data-stu-id="cebd7-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="cebd7-190">Verificare che gli avvisi definiti per i pool elastici usino un periodo (WindowSize) di almeno 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="cebd7-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="cebd7-191">Questo esempio viene aggiunto un avviso tooeach dei database hello in un pool elastico per ricevere notifiche quando il consumo di DTU del database supera determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="cebd7-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="cebd7-192">Raccogliere e monitorare i dati sull'utilizzo delle risorse in più pool in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cebd7-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="cebd7-193">Quando si dispone di molti database in una sottoscrizione, è scomodo toomonitor ogni elastica pool separatamente.</span><span class="sxs-lookup"><span data-stu-id="cebd7-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="cebd7-194">Al contrario, i cmdlet PowerShell di database SQL e query T-SQL possono essere toocollect combinati i dati di utilizzo di risorse di più pool e i relativi database per il monitoraggio e analisi dell'utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="cebd7-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="cebd7-195">Oggetto [implementazione di esempio](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) di un set di questo tipo di powershell script è reperibile nel repository di esempi di hello GitHub SQL Server insieme documentazione su vengono eseguite e come toouse è.</span><span class="sxs-lookup"><span data-stu-id="cebd7-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="cebd7-196">toouse questa implementazione di esempio, eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="cebd7-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="cebd7-197">Scaricare hello [script e la documentazione](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="cebd7-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="cebd7-198">Modificare gli script hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="cebd7-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="cebd7-199">Specificare uno o più server in cui sono ospitati i pool elastici.</span><span class="sxs-lookup"><span data-stu-id="cebd7-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="cebd7-200">Specificare un database di telemetria in hello metriche raccolte sono toobe archiviati.</span><span class="sxs-lookup"><span data-stu-id="cebd7-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="cebd7-201">Personalizzare hello script toospecify hello Durata esecuzione degli script hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="cebd7-202">In generale, gli script hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="cebd7-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="cebd7-203">Enumera tutti i server in una determinata sottoscrizione di Azure (o in determinato elenco di server).</span><span class="sxs-lookup"><span data-stu-id="cebd7-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="cebd7-204">Esegue un processo in background per ogni server.</span><span class="sxs-lookup"><span data-stu-id="cebd7-204">Runs a background job for each server.</span></span> <span data-ttu-id="cebd7-205">il processo di Hello viene eseguito in un ciclo a intervalli regolari e raccoglie i dati di telemetria per tutti i pool di hello in server hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="cebd7-206">Quindi carica hello raccolti dati nel database specificato telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="cebd7-207">Enumera un elenco di database in ogni pool toocollect hello database risorse sull'utilizzo di dati.</span><span class="sxs-lookup"><span data-stu-id="cebd7-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="cebd7-208">Quindi carica hello raccolti dati nel database di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="cebd7-209">Hello metriche raccolte nel database di telemetria hello possono essere analizzati toomonitor hello integrità del pool elastico e database hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="cebd7-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="cebd7-210">script Hello installa anche una funzione con valori di tabella predefinita (TVF) in metriche hello telemetria database toohelp hello aggregazione per un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="cebd7-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="cebd7-211">Ad esempio, possono essere i risultati di hello TVF utilizzato tooshow "top N pool elastici con l'utilizzo di eDTU massimo hello in un determinato intervallo di tempo."</span><span class="sxs-lookup"><span data-stu-id="cebd7-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="cebd7-212">Facoltativamente, usare strumenti analitici come Excel o Power BI tooquery e analizzare i dati raccolti hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="cebd7-213">Esempio: recuperare le metriche di consumo di risorse per un pool elastico e i relativi database</span><span class="sxs-lookup"><span data-stu-id="cebd7-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="cebd7-214">In questo esempio recupera le metriche di utilizzo hello per un determinato pool elastico e tutti i database.</span><span class="sxs-lookup"><span data-stu-id="cebd7-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="cebd7-215">I dati raccolti sono formattati e scritti tooa file in formato CSV.</span><span class="sxs-lookup"><span data-stu-id="cebd7-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="cebd7-216">file Hello può essere visualizzati con Excel.</span><span class="sxs-lookup"><span data-stu-id="cebd7-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
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

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="cebd7-217">Latenza delle operazioni dei pool elastici</span><span class="sxs-lookup"><span data-stu-id="cebd7-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="cebd7-218">Modifica hello min Edtu per database o un numero massimo di Edtu per ogni database in genere viene completata entro 5 minuti o meno.</span><span class="sxs-lookup"><span data-stu-id="cebd7-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="cebd7-219">Modifica hello Edtu per pool dipende dalla quantità totale di hello dello spazio utilizzato da tutti i database nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="cebd7-220">Le modifiche richiedono una media di 90 minuti o meno per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="cebd7-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="cebd7-221">Ad esempio, se lo spazio totale hello utilizzato da tutti i database nel pool di hello è 200 GB, quindi hello prevista latenza per la modifica hello pool eDTU per pool è 3 ore o minore.</span><span class="sxs-lookup"><span data-stu-id="cebd7-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cebd7-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cebd7-222">Next steps</span></span>
* <span data-ttu-id="cebd7-223">[Creare processi elastici](sql-database-elastic-jobs-overview.md) elastici processi consentono di eseguire script T-SQL in un numero qualsiasi di database nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="cebd7-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="cebd7-224">Vedere [scalabilità orizzontale con Database SQL di Azure](sql-database-elastic-scale-introduction.md): utilizzare strumenti elastico tooscale out, spostare i dati, eseguire una query o creare transazioni.</span><span class="sxs-lookup"><span data-stu-id="cebd7-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
