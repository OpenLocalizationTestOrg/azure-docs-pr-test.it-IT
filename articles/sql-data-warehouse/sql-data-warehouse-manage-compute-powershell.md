---
title: aaaManage calcolo power in Azure SQL Data Warehouse (PowerShell) | Documenti Microsoft
description: "Potenza di calcolo toomanage attività PowerShell. Ridimensionare le risorse di calcolo cambiando il numero di DWU. In alternativa, è possibile sospendere e riprendere toosave costi delle risorse di calcolo."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>Gestire la potenza di calcolo in Azure SQL Data Warehouse (PowerShell)
> [!div class="op_single_selector"]
> * [Panoramica](sql-data-warehouse-manage-compute-overview.md)
> * [Portale](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>Prima di iniziare
### <a name="install-hello-latest-version-of-azure-powershell"></a>Installare hello la versione più recente di Azure PowerShell
> [!NOTE]
> toouse PowerShell di Azure con SQL Data Warehouse, è necessario Azure PowerShell versione 1.0.3 o versione successiva.  tooverify la versione corrente comando hello **Get-Module - ListAvailable-Name Azure**. È possibile installare una versione più recente di hello dal [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].  Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>Introduzione ai cmdlet di Azure PowerShell
tooget avviato:

1. Aprire Azure PowerShell.
2. Al prompt di PowerShell hello, eseguire questi comandi toosign in toohello Gestione risorse di Azure e selezionare la sottoscrizione.

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>Ridimensionare la potenza di calcolo
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

hello toochange Dwu, utilizzare hello [Set AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] cmdlet di PowerShell. Hello esempio imposta hello servizio livello obiettivo tooDW1000 per database hello MySQLDW che è ospitato nel server MyServer.

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Sospendere le risorse di calcolo
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause un database, utilizzare hello [Suspend AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet. Hello esempio seguente viene sospeso un database denominato Database02 ospitato in un server denominato Server01. server Hello è denominato ResourceGroup1 in un gruppo di risorse di Azure.

> [!NOTE]
> Si noti che se il server è foo.database.windows.net, utilizzare "foo" come hello - ServerName nei cmdlet di PowerShell hello.
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
Una variazione, in questo esempio Recupera database hello in oggetto hello $database. Quindi, Invia oggetto hello troppo[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]. Hello risultati vengono archiviati in resultDatabase oggetto hello. comando finale Hello Mostra risultati hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Riavviare le risorse di calcolo
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart un database, utilizzare hello [Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet. Hello esempio seguente viene avviato un database denominato Database02 ospitato in un server denominato Server01. server Hello è denominato ResourceGroup1 in un gruppo di risorse di Azure.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

Una variazione, in questo esempio Recupera database hello in oggetto hello $database. Quindi, Invia oggetto hello troppo[Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] e archivia i risultati di hello in $resultDatabase. comando finale Hello Mostra risultati hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>Controllare lo stato del database

Come illustrato nell'hello esempi sopra riportati, è possibile utilizzare [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget informazioni in un database, in tal modo il controllo stato hello, ma anche toouse come argomento. 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

Verrà visualizzato un risultato simile al seguente: 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

In cui è possibile selezionare hello toosee *stato* del database hello. Nel caso in questione, il database è online. 

Quando si esegue questo comando, è possibile ricevere un valore di stato Online, In pausa, Ripresa, Ridimensionamento e Sospeso.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Passaggi successivi
Per altre attività di gestione, vedere [Panoramica della gestione][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
