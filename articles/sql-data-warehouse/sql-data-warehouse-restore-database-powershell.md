---
title: aaaRestore un Azure SQL Data Warehouse (PowerShell) | Documenti Microsoft
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
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="b81fa-103">Ripristinare un'istanza di Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="b81fa-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b81fa-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="b81fa-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b81fa-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="b81fa-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="b81fa-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="b81fa-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="b81fa-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="b81fa-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="b81fa-108">In questo articolo si apprenderà come toorestore un Azure SQL Data Warehouse tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b81fa-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b81fa-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b81fa-109">Before you begin</span></span>
<span data-ttu-id="b81fa-110">**Verificare la capacità in DTU.**</span><span class="sxs-lookup"><span data-stu-id="b81fa-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="b81fa-111">Ogni SQL Data Warehouse è ospitato in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota DTU predefinita.</span><span class="sxs-lookup"><span data-stu-id="b81fa-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="b81fa-112">Prima di poter ripristinare un SQL Data Warehouse, verificare che hello che di SQL server è sufficientemente rimanente quota DTU per database hello da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="b81fa-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="b81fa-113">toolearn come toocalculate DTU necessarie o toorequest più DTU, vedere [richiedere una modifica della quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="b81fa-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="b81fa-114">Installare PowerShell</span><span class="sxs-lookup"><span data-stu-id="b81fa-114">Install PowerShell</span></span>
<span data-ttu-id="b81fa-115">In ordine toouse PowerShell di Azure con SQL Data Warehouse, sarà necessario tooinstall Azure PowerShell versione 1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b81fa-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="b81fa-116">Per controllare la versione usata, eseguire **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="b81fa-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="b81fa-117">è possibile installare la versione più recente di Hello da [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="b81fa-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="b81fa-118">Per ulteriori informazioni su come installare la versione più recente di hello, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="b81fa-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="b81fa-119">Ripristinare un database attivo o sospeso</span><span class="sxs-lookup"><span data-stu-id="b81fa-119">Restore an active or paused database</span></span>
<span data-ttu-id="b81fa-120">un database da uno snapshot toorestore utilizzare hello [ripristino AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b81fa-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="b81fa-121">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b81fa-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b81fa-122">Connettersi tooyour account Azure ed elencare tutte le sottoscrizioni di hello associate all'account.</span><span class="sxs-lookup"><span data-stu-id="b81fa-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b81fa-123">Selezionare sottoscrizione hello contenente hello toobe di database ripristinato.</span><span class="sxs-lookup"><span data-stu-id="b81fa-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="b81fa-124">Hello elenco ripristinare i punti per database hello.</span><span class="sxs-lookup"><span data-stu-id="b81fa-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="b81fa-125">Selezionare il punto di ripristino hello desiderato utilizzando hello RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="b81fa-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="b81fa-126">Punto di ripristino hello database toohello desiderato di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b81fa-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="b81fa-127">Verificare che il database ripristinato hello è online.</span><span class="sxs-lookup"><span data-stu-id="b81fa-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="b81fa-128">Al termine del ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b81fa-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="b81fa-129">Ripristino di un database eliminato</span><span class="sxs-lookup"><span data-stu-id="b81fa-129">Restore a deleted database</span></span>
<span data-ttu-id="b81fa-130">toorestore un database eliminato, utilizzare hello [ripristino AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b81fa-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="b81fa-131">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b81fa-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b81fa-132">Connettersi tooyour account Azure ed elencare tutte le sottoscrizioni di hello associate all'account.</span><span class="sxs-lookup"><span data-stu-id="b81fa-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b81fa-133">Eliminare la sottoscrizione selezionare hello contenente hello toobe database ripristinato.</span><span class="sxs-lookup"><span data-stu-id="b81fa-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="b81fa-134">Ottenere i database eliminato hello specifico.</span><span class="sxs-lookup"><span data-stu-id="b81fa-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="b81fa-135">Ripristinare il database di hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="b81fa-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="b81fa-136">Verificare che il database ripristinato hello è online.</span><span class="sxs-lookup"><span data-stu-id="b81fa-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="b81fa-137">Al termine del ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b81fa-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="b81fa-138">Eseguire il ripristino da un'area geografica di Azure</span><span class="sxs-lookup"><span data-stu-id="b81fa-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="b81fa-139">toorecover un database, utilizzare hello [ripristino AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b81fa-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="b81fa-140">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b81fa-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b81fa-141">Connettersi tooyour account Azure ed elencare tutte le sottoscrizioni di hello associate all'account.</span><span class="sxs-lookup"><span data-stu-id="b81fa-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b81fa-142">Selezionare sottoscrizione hello contenente hello toobe di database ripristinato.</span><span class="sxs-lookup"><span data-stu-id="b81fa-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="b81fa-143">Ottenere il database di hello da toorecover.</span><span class="sxs-lookup"><span data-stu-id="b81fa-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="b81fa-144">Creare una richiesta di ripristino hello per database hello.</span><span class="sxs-lookup"><span data-stu-id="b81fa-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="b81fa-145">Verificare lo stato di hello del database ripristinato geografica hello.</span><span class="sxs-lookup"><span data-stu-id="b81fa-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="b81fa-146">vedere il database al termine del ripristino di hello, tooconfigure [configura il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b81fa-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="b81fa-147">database ripristinato Hello sarà abilitato per TDE se il database di origine di hello è abilitato per TDE.</span><span class="sxs-lookup"><span data-stu-id="b81fa-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b81fa-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b81fa-148">Next steps</span></span>
<span data-ttu-id="b81fa-149">toolearn sulle funzionalità di continuità aziendale hello delle edizioni di Database SQL di Azure, leggere hello [Panoramica di continuità aziendale di Database SQL di Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="b81fa-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
