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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="0fe78-105">Gestire la potenza di calcolo in Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0fe78-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fe78-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0fe78-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="0fe78-107">Portale</span><span class="sxs-lookup"><span data-stu-id="0fe78-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="0fe78-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fe78-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="0fe78-109">REST</span><span class="sxs-lookup"><span data-stu-id="0fe78-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="0fe78-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="0fe78-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="0fe78-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0fe78-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="0fe78-112">Installare hello la versione più recente di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fe78-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="0fe78-113">toouse PowerShell di Azure con SQL Data Warehouse, è necessario Azure PowerShell versione 1.0.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0fe78-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="0fe78-114">tooverify la versione corrente comando hello **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="0fe78-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="0fe78-115">È possibile installare una versione più recente di hello dal [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="0fe78-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="0fe78-116">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="0fe78-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="0fe78-117">Introduzione ai cmdlet di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fe78-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="0fe78-118">tooget avviato:</span><span class="sxs-lookup"><span data-stu-id="0fe78-118">tooget started:</span></span>

1. <span data-ttu-id="0fe78-119">Aprire Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fe78-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="0fe78-120">Al prompt di PowerShell hello, eseguire questi comandi toosign in toohello Gestione risorse di Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0fe78-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="0fe78-121">Ridimensionare la potenza di calcolo</span><span class="sxs-lookup"><span data-stu-id="0fe78-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="0fe78-122">hello toochange Dwu, utilizzare hello [Set AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fe78-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="0fe78-123">Hello esempio imposta hello servizio livello obiettivo tooDW1000 per database hello MySQLDW che è ospitato nel server MyServer.</span><span class="sxs-lookup"><span data-stu-id="0fe78-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="0fe78-124">Sospendere le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="0fe78-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="0fe78-125">toopause un database, utilizzare hello [Suspend AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0fe78-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="0fe78-126">Hello esempio seguente viene sospeso un database denominato Database02 ospitato in un server denominato Server01.</span><span class="sxs-lookup"><span data-stu-id="0fe78-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="0fe78-127">server Hello è denominato ResourceGroup1 in un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe78-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="0fe78-128">Si noti che se il server è foo.database.windows.net, utilizzare "foo" come hello - ServerName nei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0fe78-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="0fe78-129">Una variazione, in questo esempio Recupera database hello in oggetto hello $database.</span><span class="sxs-lookup"><span data-stu-id="0fe78-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="0fe78-130">Quindi, Invia oggetto hello troppo[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="0fe78-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="0fe78-131">Hello risultati vengono archiviati in resultDatabase oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="0fe78-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="0fe78-132">comando finale Hello Mostra risultati hello.</span><span class="sxs-lookup"><span data-stu-id="0fe78-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="0fe78-133">Riavviare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="0fe78-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="0fe78-134">toostart un database, utilizzare hello [Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0fe78-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="0fe78-135">Hello esempio seguente viene avviato un database denominato Database02 ospitato in un server denominato Server01.</span><span class="sxs-lookup"><span data-stu-id="0fe78-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="0fe78-136">server Hello è denominato ResourceGroup1 in un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe78-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="0fe78-137">Una variazione, in questo esempio Recupera database hello in oggetto hello $database.</span><span class="sxs-lookup"><span data-stu-id="0fe78-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="0fe78-138">Quindi, Invia oggetto hello troppo[Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] e archivia i risultati di hello in $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="0fe78-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="0fe78-139">comando finale Hello Mostra risultati hello.</span><span class="sxs-lookup"><span data-stu-id="0fe78-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="0fe78-140">Controllare lo stato del database</span><span class="sxs-lookup"><span data-stu-id="0fe78-140">Check database state</span></span>

<span data-ttu-id="0fe78-141">Come illustrato nell'hello esempi sopra riportati, è possibile utilizzare [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget informazioni in un database, in tal modo il controllo stato hello, ma anche toouse come argomento.</span><span class="sxs-lookup"><span data-stu-id="0fe78-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="0fe78-142">Verrà visualizzato un risultato simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0fe78-142">Which will result in something like</span></span> 

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

<span data-ttu-id="0fe78-143">In cui è possibile selezionare hello toosee *stato* del database hello.</span><span class="sxs-lookup"><span data-stu-id="0fe78-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="0fe78-144">Nel caso in questione, il database è online.</span><span class="sxs-lookup"><span data-stu-id="0fe78-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="0fe78-145">Quando si esegue questo comando, è possibile ricevere un valore di stato Online, In pausa, Ripresa, Ridimensionamento e Sospeso.</span><span class="sxs-lookup"><span data-stu-id="0fe78-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="0fe78-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0fe78-146">Next steps</span></span>
<span data-ttu-id="0fe78-147">Per altre attività di gestione, vedere [Panoramica della gestione][Management overview].</span><span class="sxs-lookup"><span data-stu-id="0fe78-147">For other management tasks, see [Management overview][Management overview].</span></span>

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
