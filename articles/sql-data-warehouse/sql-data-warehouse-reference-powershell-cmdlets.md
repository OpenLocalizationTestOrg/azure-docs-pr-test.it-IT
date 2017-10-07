---
title: cmdlet aaaPowerShell per Azure SQL Data Warehouse
description: Trovare hello superiore dei cmdlet di PowerShell per Azure SQL Data Warehouse e come toopause e riprendere un database.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>Usare i cmdlet di PowerShell e le API REST con SQL Data Warehouse
Molte attività di amministrazione di SQL Data Warehouse possono essere gestite tramite i cmdlet di Azure PowerShell o le API REST.  Di seguito sono riportati alcuni esempi del funzionamento dei comandi PowerShell toouse tooautomate attività comuni in SQL Data Warehouse.  Per altri esempi, vedere l'articolo hello [gestire la scalabilità con REST][Manage scalability with REST].

> [!NOTE]
> In ordine toouse PowerShell di Azure con SQL Data Warehouse, è necessario Azure PowerShell versione 1.0.3 o versione successiva.  È possibile controllare la versione in uso eseguendo **Get-Module -ListAvailable -Name Azure**.  è possibile installare la versione più recente di Hello da [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].  Per ulteriori informazioni su come installare la versione più recente di hello, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Introduzione ai cmdlet di Azure PowerShell
1. Aprire Windows PowerShell.
2. Al prompt di PowerShell hello, eseguire questi comandi toosign in toohello Gestione risorse di Azure e selezionare la sottoscrizione.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>Esempio di sospensione di SQL Data Warehouse
Sospende un database denominato "Database02" ospitato su un server denominato "Server01".  Hello server si trova in un gruppo di risorse di Azure denominato "ResourceGroup1".

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
Una variazione, in questo esempio invia tramite pipe oggetti recuperato hello troppo[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].  Di conseguenza, i database di hello è sospesa. comando finale Hello Mostra risultati hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>Esempio di avvio di SQL Data Warehouse
Fa riprendere le operazioni di un database denominato "Database02" ospitato su un server denominato "Server01". server Hello è contenuto in un gruppo di risorse denominato "ResourceGroup1".

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

Come variazione, questo esempio recupera un database denominato "Database02" da un server denominato "Server01" incluso in un gruppo di risorse denominato "ResourceGroup1". Invia tramite pipe oggetti recuperato hello troppo[Resume AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> Si noti che se il server è foo.database.windows.net, utilizzare "foo" come hello - ServerName nei cmdlet di PowerShell hello.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>Altri cmdlet di PowerShell supportati
Questi cmdlet di PowerShell sono supportati con Azure SQL Data Warehouse.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [Select-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>Passaggi successivi
Per altri esempi di PowerShell, vedere:

* [Creare SQL Data Warehouse con PowerShell][Create a SQL Data Warehouse using PowerShell]
* [Ripristino del database][Database restore]

Per le altre attività che possono essere automatizzate con PowerShell, vedere [Cmdlet del database SQL di Azure][Azure SQL Database Cmdlets]. Si noti che non tutti i cmdlet del database SQL di Azure sono supportati per Azure SQL Data Warehouse.  Per un elenco di attività che possono essere automatizzate con REST, vedere [Operazioni per i database SQL di Azure][Operations for Azure SQL Databases].

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
