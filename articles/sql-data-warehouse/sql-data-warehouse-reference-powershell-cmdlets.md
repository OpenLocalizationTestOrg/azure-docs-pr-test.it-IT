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
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="258ce-103">Usare i cmdlet di PowerShell e le API REST con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="258ce-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="258ce-104">Molte attività di amministrazione di SQL Data Warehouse possono essere gestite tramite i cmdlet di Azure PowerShell o le API REST.</span><span class="sxs-lookup"><span data-stu-id="258ce-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="258ce-105">Di seguito sono riportati alcuni esempi del funzionamento dei comandi PowerShell toouse tooautomate attività comuni in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="258ce-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="258ce-106">Per altri esempi, vedere l'articolo hello [gestire la scalabilità con REST][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="258ce-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="258ce-107">In ordine toouse PowerShell di Azure con SQL Data Warehouse, è necessario Azure PowerShell versione 1.0.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="258ce-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="258ce-108">È possibile controllare la versione in uso eseguendo **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="258ce-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="258ce-109">è possibile installare la versione più recente di Hello da [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="258ce-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="258ce-110">Per ulteriori informazioni su come installare la versione più recente di hello, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="258ce-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="258ce-111">Introduzione ai cmdlet di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="258ce-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="258ce-112">Aprire Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="258ce-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="258ce-113">Al prompt di PowerShell hello, eseguire questi comandi toosign in toohello Gestione risorse di Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="258ce-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="258ce-114">Esempio di sospensione di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="258ce-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="258ce-115">Sospende un database denominato "Database02" ospitato su un server denominato "Server01".</span><span class="sxs-lookup"><span data-stu-id="258ce-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="258ce-116">Hello server si trova in un gruppo di risorse di Azure denominato "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="258ce-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="258ce-117">Una variazione, in questo esempio invia tramite pipe oggetti recuperato hello troppo[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="258ce-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="258ce-118">Di conseguenza, i database di hello è sospesa.</span><span class="sxs-lookup"><span data-stu-id="258ce-118">As a result, hello database is paused.</span></span> <span data-ttu-id="258ce-119">comando finale Hello Mostra risultati hello.</span><span class="sxs-lookup"><span data-stu-id="258ce-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="258ce-120">Esempio di avvio di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="258ce-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="258ce-121">Fa riprendere le operazioni di un database denominato "Database02" ospitato su un server denominato "Server01".</span><span class="sxs-lookup"><span data-stu-id="258ce-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="258ce-122">server Hello è contenuto in un gruppo di risorse denominato "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="258ce-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="258ce-123">Come variazione, questo esempio recupera un database denominato "Database02" da un server denominato "Server01" incluso in un gruppo di risorse denominato "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="258ce-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="258ce-124">Invia tramite pipe oggetti recuperato hello troppo[Resume AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="258ce-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="258ce-125">Si noti che se il server è foo.database.windows.net, utilizzare "foo" come hello - ServerName nei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="258ce-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="258ce-126">Altri cmdlet di PowerShell supportati</span><span class="sxs-lookup"><span data-stu-id="258ce-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="258ce-127">Questi cmdlet di PowerShell sono supportati con Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="258ce-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="258ce-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="258ce-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="258ce-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="258ce-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="258ce-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="258ce-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="258ce-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="258ce-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="258ce-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="258ce-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="258ce-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="258ce-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="258ce-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="258ce-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="258ce-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="258ce-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="258ce-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="258ce-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="258ce-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="258ce-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="258ce-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="258ce-138">Next steps</span></span>
<span data-ttu-id="258ce-139">Per altri esempi di PowerShell, vedere:</span><span class="sxs-lookup"><span data-stu-id="258ce-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="258ce-140">[Creare SQL Data Warehouse con PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="258ce-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="258ce-141">[Ripristino del database][Database restore]</span><span class="sxs-lookup"><span data-stu-id="258ce-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="258ce-142">Per le altre attività che possono essere automatizzate con PowerShell, vedere [Cmdlet del database SQL di Azure][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="258ce-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="258ce-143">Si noti che non tutti i cmdlet del database SQL di Azure sono supportati per Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="258ce-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="258ce-144">Per un elenco di attività che possono essere automatizzate con REST, vedere [Operazioni per i database SQL di Azure][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="258ce-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

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
