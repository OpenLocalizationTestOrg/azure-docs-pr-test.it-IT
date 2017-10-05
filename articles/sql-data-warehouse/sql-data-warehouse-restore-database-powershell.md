---
title: Ripristinare un'istanza di Azure SQL Data Warehouse (PowerShell) | Documentazione Microsoft
description: "Attività di PowerShell per il ripristino di un'istanza di Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="318f5-103">Ripristinare un'istanza di Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="318f5-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="318f5-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="318f5-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="318f5-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="318f5-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="318f5-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="318f5-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="318f5-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="318f5-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="318f5-108">Questo articolo illustra come ripristinare un'istanza di Azure SQL Data Warehouse usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="318f5-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="318f5-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="318f5-109">Before you begin</span></span>
<span data-ttu-id="318f5-110">**Verificare la capacità in DTU.**</span><span class="sxs-lookup"><span data-stu-id="318f5-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="318f5-111">Ogni SQL Data Warehouse è ospitato in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota DTU predefinita.</span><span class="sxs-lookup"><span data-stu-id="318f5-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="318f5-112">Per poter ripristinare un SQL Data Warehouse, verificare che la quota DTU rimanente nell'istanza del server SQL sia sufficiente per il database da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="318f5-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="318f5-113">Per informazioni su come calcolare la DTU necessaria o per richiedere altre DTU, vedere come [richiedere una modifica della quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="318f5-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="318f5-114">Installare PowerShell</span><span class="sxs-lookup"><span data-stu-id="318f5-114">Install PowerShell</span></span>
<span data-ttu-id="318f5-115">Per usare Azure PowerShell con SQL Data Warehouse, è necessario installare Azure PowerShell versione 1.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="318f5-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="318f5-116">Per controllare la versione usata, eseguire **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="318f5-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="318f5-117">È possibile installare la versione più recente usando [Installazione guidata piattaforma Web Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="318f5-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="318f5-118">Per altre informazioni sull'installazione della versione più recente, vedere [Come installare e configurare Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="318f5-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="318f5-119">Ripristinare un database attivo o sospeso</span><span class="sxs-lookup"><span data-stu-id="318f5-119">Restore an active or paused database</span></span>
<span data-ttu-id="318f5-120">Per ripristinare un database da uno snapshot, usare il cmdlet di PowerShell [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="318f5-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="318f5-121">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="318f5-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="318f5-122">Connettersi al proprio account Azure ed elencare tutte le sottoscrizioni associate all'account.</span><span class="sxs-lookup"><span data-stu-id="318f5-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="318f5-123">Selezionare la sottoscrizione che contiene il database da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="318f5-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="318f5-124">Specificare i punti di ripristino per il database.</span><span class="sxs-lookup"><span data-stu-id="318f5-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="318f5-125">Selezionare il punto di ripristino desiderato utilizzando RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="318f5-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="318f5-126">Ripristinare il database al punto di ripristino desiderato.</span><span class="sxs-lookup"><span data-stu-id="318f5-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="318f5-127">Verificare che il database ripristinato sia online.</span><span class="sxs-lookup"><span data-stu-id="318f5-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="318f5-128">Al termine del ripristino sarà possibile configurare il database ripristinato seguendo le istruzioni disponibili in [Configurare il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="318f5-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="318f5-129">Ripristino di un database eliminato</span><span class="sxs-lookup"><span data-stu-id="318f5-129">Restore a deleted database</span></span>
<span data-ttu-id="318f5-130">Per ripristinare un database eliminato, usare il cmdlet [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="318f5-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="318f5-131">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="318f5-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="318f5-132">Connettersi al proprio account Azure ed elencare tutte le sottoscrizioni associate all'account.</span><span class="sxs-lookup"><span data-stu-id="318f5-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="318f5-133">Selezionare la sottoscrizione che contiene il database eliminato da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="318f5-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="318f5-134">Specificare il database eliminato.</span><span class="sxs-lookup"><span data-stu-id="318f5-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="318f5-135">Ripristinare il database eliminato.</span><span class="sxs-lookup"><span data-stu-id="318f5-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="318f5-136">Verificare che il database ripristinato sia online.</span><span class="sxs-lookup"><span data-stu-id="318f5-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="318f5-137">Al termine del ripristino sarà possibile configurare il database ripristinato seguendo le istruzioni disponibili in [Configurare il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="318f5-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="318f5-138">Eseguire il ripristino da un'area geografica di Azure</span><span class="sxs-lookup"><span data-stu-id="318f5-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="318f5-139">Per ripristinare un database, usare il cmdlet [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="318f5-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="318f5-140">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="318f5-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="318f5-141">Connettersi al proprio account Azure ed elencare tutte le sottoscrizioni associate all'account.</span><span class="sxs-lookup"><span data-stu-id="318f5-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="318f5-142">Selezionare la sottoscrizione che contiene il database da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="318f5-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="318f5-143">Selezionare il database che si desidera ripristinare.</span><span class="sxs-lookup"><span data-stu-id="318f5-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="318f5-144">Creare la richiesta di ripristino per il database.</span><span class="sxs-lookup"><span data-stu-id="318f5-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="318f5-145">Verificare lo stato del database recuperato con il ripristino geografico.</span><span class="sxs-lookup"><span data-stu-id="318f5-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="318f5-146">Per configurare il database al termine del ripristino, vedere [Configurare il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="318f5-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="318f5-147">Il database ripristinato sarà abilitato TDE se il database di origine è abilitato per questa tecnologia.</span><span class="sxs-lookup"><span data-stu-id="318f5-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="318f5-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="318f5-148">Next steps</span></span>
<span data-ttu-id="318f5-149">Per altre informazioni sulle funzionalità di continuità aziendale delle edizioni del database SQL di Azure, vedere [Panoramica sulla continuità aziendale del database SQL di Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="318f5-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
