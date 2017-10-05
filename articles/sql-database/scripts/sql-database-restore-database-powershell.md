---
title: Esempio di PowerShell - Ripristinare un backup del database SQL di Azure | Microsoft Docs
description: Script di esempio di Azure PowerShell per ripristinare un database SQL di Azure da backup con ridondanza geografica
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae1d0c828ae1e7e1e7e07dcc7d6157187a3859d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="576c1-103">Usare PowerShell per ripristinare un database SQL di Azure dai backup</span><span class="sxs-lookup"><span data-stu-id="576c1-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="576c1-104">Questo esempio di script di PowerShell ripristina un database SQL di Azure da un backup con ridondanza geografica, ripristina un database SQL di Azure eliminato in base al backup più recente ed esegue un ripristino temporizzato di un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="576c1-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="576c1-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="576c1-105">Sample script</span></span>

<span data-ttu-id="576c1-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Creare database SQL")]</span><span class="sxs-lookup"><span data-stu-id="576c1-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="576c1-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="576c1-107">Clean up deployment</span></span>

<span data-ttu-id="576c1-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="576c1-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="576c1-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="576c1-109">Script explanation</span></span>

<span data-ttu-id="576c1-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="576c1-110">This script uses the following commands.</span></span> <span data-ttu-id="576c1-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="576c1-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="576c1-112">Comando</span><span class="sxs-lookup"><span data-stu-id="576c1-112">Command</span></span> | <span data-ttu-id="576c1-113">Note</span><span class="sxs-lookup"><span data-stu-id="576c1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="576c1-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="576c1-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="576c1-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="576c1-115">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="576c1-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="576c1-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="576c1-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="576c1-117">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="576c1-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="576c1-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="576c1-119">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="576c1-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="576c1-120">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="576c1-120">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="576c1-121">Ottiene una copia di backup con ridondanza geografica di un database.</span><span class="sxs-lookup"><span data-stu-id="576c1-121">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="576c1-122">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="576c1-122">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="576c1-123">Ripristina un database SQL.</span><span class="sxs-lookup"><span data-stu-id="576c1-123">Restores a SQL database.</span></span> |
|[<span data-ttu-id="576c1-124">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="576c1-124">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="576c1-125">Rimuove un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="576c1-125">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="576c1-126">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="576c1-126">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="576c1-127">Ottiene un database eliminato che è possibile ripristinare.</span><span class="sxs-lookup"><span data-stu-id="576c1-127">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="576c1-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="576c1-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="576c1-129">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="576c1-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="576c1-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="576c1-130">Next steps</span></span>

<span data-ttu-id="576c1-131">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="576c1-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="576c1-132">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="576c1-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
