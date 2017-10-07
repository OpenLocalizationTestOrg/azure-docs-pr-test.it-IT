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
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Ripristinare un'istanza di Azure SQL Data Warehouse (PowerShell)
> [!div class="op_single_selector"]
> * [Panoramica][Overview]
> * [Portale][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

In questo articolo si apprenderà come toorestore un Azure SQL Data Warehouse tramite PowerShell.

## <a name="before-you-begin"></a>Prima di iniziare
**Verificare la capacità in DTU.** Ogni SQL Data Warehouse è ospitato in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota DTU predefinita.  Prima di poter ripristinare un SQL Data Warehouse, verificare che hello che di SQL server è sufficientemente rimanente quota DTU per database hello da ripristinare. toolearn come toocalculate DTU necessarie o toorequest più DTU, vedere [richiedere una modifica della quota DTU][Request a DTU quota change].

### <a name="install-powershell"></a>Installare PowerShell
In ordine toouse PowerShell di Azure con SQL Data Warehouse, sarà necessario tooinstall Azure PowerShell versione 1.0 o versione successiva.  Per controllare la versione usata, eseguire **Get-Module -ListAvailable -Name AzureRM**.  è possibile installare la versione più recente di Hello da [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].  Per ulteriori informazioni su come installare la versione più recente di hello, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Ripristinare un database attivo o sospeso
un database da uno snapshot toorestore utilizzare hello [ripristino AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet di PowerShell.

1. Aprire Windows PowerShell.
2. Connettersi tooyour account Azure ed elencare tutte le sottoscrizioni di hello associate all'account.
3. Selezionare sottoscrizione hello contenente hello toobe di database ripristinato.
4. Hello elenco ripristinare i punti per database hello.
5. Selezionare il punto di ripristino hello desiderato utilizzando hello RestorePointCreationDate.
6. Punto di ripristino hello database toohello desiderato di ripristino.
7. Verificare che il database ripristinato hello è online.

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
> Al termine del ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Ripristino di un database eliminato
toorestore un database eliminato, utilizzare hello [ripristino AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Aprire Windows PowerShell.
2. Connettersi tooyour account Azure ed elencare tutte le sottoscrizioni di hello associate all'account.
3. Eliminare la sottoscrizione selezionare hello contenente hello toobe database ripristinato.
4. Ottenere i database eliminato hello specifico.
5. Ripristinare il database di hello eliminato.
6. Verificare che il database ripristinato hello è online.

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
> Al termine del ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Eseguire il ripristino da un'area geografica di Azure
toorecover un database, utilizzare hello [ripristino AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Aprire Windows PowerShell.
2. Connettersi tooyour account Azure ed elencare tutte le sottoscrizioni di hello associate all'account.
3. Selezionare sottoscrizione hello contenente hello toobe di database ripristinato.
4. Ottenere il database di hello da toorecover.
5. Creare una richiesta di ripristino hello per database hello.
6. Verificare lo stato di hello del database ripristinato geografica hello.

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
> vedere il database al termine del ripristino di hello, tooconfigure [configura il database dopo il ripristino][Configure your database after recovery].
> 
> 

database ripristinato Hello sarà abilitato per TDE se il database di origine di hello è abilitato per TDE.

## <a name="next-steps"></a>Passaggi successivi
toolearn sulle funzionalità di continuità aziendale hello delle edizioni di Database SQL di Azure, leggere hello [Panoramica di continuità aziendale di Database SQL di Azure][Azure SQL Database business continuity overview].

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
