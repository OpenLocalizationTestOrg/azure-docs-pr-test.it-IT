---
title: Gestire la potenza di calcolo in Azure SQL Data Warehouse (PowerShell) | Microsoft Docs
description: "Attività di PowerShell per la gestione della potenza di calcolo. Ridimensionare le risorse di calcolo cambiando il numero di DWU. In alternativa, sospendere e riprendere le risorse di calcolo per ridurre i costi."
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
ms.openlocfilehash: 6a185d96447c2e1b0b463439dd062081e783da5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="e665f-105">Gestire la potenza di calcolo in Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e665f-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e665f-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e665f-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="e665f-107">Portale</span><span class="sxs-lookup"><span data-stu-id="e665f-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="e665f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e665f-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="e665f-109">REST</span><span class="sxs-lookup"><span data-stu-id="e665f-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="e665f-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="e665f-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="e665f-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e665f-111">Before you begin</span></span>
### <a name="install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="e665f-112">Installare la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e665f-112">Install the latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="e665f-113">Per usare Azure PowerShell con SQL Data Warehouse, è necessario installare Azure PowerShell 1.0.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e665f-113">To use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="e665f-114">Per verificare la versione corrente, eseguire il comando **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="e665f-114">To verify your current version run the command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="e665f-115">È possibile installare la versione più recente usando l'[Installazione guidata piattaforma Web Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="e665f-115">You can install the latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="e665f-116">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="e665f-116">For more information, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="e665f-117">Introduzione ai cmdlet di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e665f-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="e665f-118">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="e665f-118">To get started:</span></span>

1. <span data-ttu-id="e665f-119">Aprire Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e665f-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="e665f-120">Al prompt di PowerShell, eseguire questi comandi per accedere ad Azure Resource Manager e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e665f-120">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="e665f-121">Ridimensionare la potenza di calcolo</span><span class="sxs-lookup"><span data-stu-id="e665f-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="e665f-122">Per modificare il numero di DWU usare il cmdlet PowerShell [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="e665f-122">To change the DWUs, use the [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="e665f-123">L'esempio seguente imposta l'obiettivo del livello di servizio su DW1000 per il database MySQLDW ospitato nel server MyServer.</span><span class="sxs-lookup"><span data-stu-id="e665f-123">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="e665f-124">Sospendere le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="e665f-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="e665f-125">Per sospendere l'esecuzione di un database, usare il cmdlet [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="e665f-125">To pause a database, use the [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="e665f-126">L'esempio seguente sospende il database Database02 ospitato sul server Server01.</span><span class="sxs-lookup"><span data-stu-id="e665f-126">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="e665f-127">Il server appartiene al gruppo di risorse di Azure ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="e665f-127">The server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="e665f-128">Se il server è foo.database.windows.net, usare "foo" come nome server nei cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e665f-128">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="e665f-129">Come variazione, il database dell'esempio seguente viene recuperato nell'oggetto $database.</span><span class="sxs-lookup"><span data-stu-id="e665f-129">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="e665f-130">L'oggetto viene quindi inviato tramite pipe a [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="e665f-130">It then pipes the object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="e665f-131">I risultati vengono archiviati nell'oggetto resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="e665f-131">The results are stored in the object resultDatabase.</span></span> <span data-ttu-id="e665f-132">Il comando finale mostra i risultati.</span><span class="sxs-lookup"><span data-stu-id="e665f-132">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="e665f-133">Riavviare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="e665f-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="e665f-134">Per avviare un database, usare il cmdlet [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="e665f-134">To start a database, use the [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="e665f-135">L'esempio seguente avvia il database Database02 ospitato sul server Server01.</span><span class="sxs-lookup"><span data-stu-id="e665f-135">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="e665f-136">Il server appartiene al gruppo di risorse di Azure ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="e665f-136">The server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="e665f-137">Come variazione, il database dell'esempio seguente viene recuperato nell'oggetto $database.</span><span class="sxs-lookup"><span data-stu-id="e665f-137">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="e665f-138">L'oggetto viene quindi inviato tramite pipe a [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] e i risultati vengono archiviati in $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="e665f-138">It then pipes the object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores the results in $resultDatabase.</span></span> <span data-ttu-id="e665f-139">Il comando finale mostra i risultati.</span><span class="sxs-lookup"><span data-stu-id="e665f-139">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="e665f-140">Controllare lo stato del database</span><span class="sxs-lookup"><span data-stu-id="e665f-140">Check database state</span></span>

<span data-ttu-id="e665f-141">Come illustrato negli esempi precedenti, è possibile usare il cmdlet [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] per ottenere informazioni su un database, controllando quindi lo stato, oppure usarlo come argomento.</span><span class="sxs-lookup"><span data-stu-id="e665f-141">As shown in the above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet to get information on a database, thereby checking the status, but also to use as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="e665f-142">Verrà visualizzato un risultato simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e665f-142">Which will result in something like</span></span> 

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

<span data-ttu-id="e665f-143">in cui è quindi possibile controllare lo *stato* del database.</span><span class="sxs-lookup"><span data-stu-id="e665f-143">Where you can then check to see the *Status* of the database.</span></span> <span data-ttu-id="e665f-144">Nel caso in questione, il database è online.</span><span class="sxs-lookup"><span data-stu-id="e665f-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="e665f-145">Quando si esegue questo comando, è possibile ricevere un valore di stato Online, In pausa, Ripresa, Ridimensionamento e Sospeso.</span><span class="sxs-lookup"><span data-stu-id="e665f-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="e665f-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e665f-146">Next steps</span></span>
<span data-ttu-id="e665f-147">Per altre attività di gestione, vedere [Panoramica della gestione][Management overview].</span><span class="sxs-lookup"><span data-stu-id="e665f-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
