---
title: database SQL di Azure backup di ripristino configurazione di esempio aaaPowerShell | Documenti Microsoft
description: Azure PowerShell esempio script toorestore un database SQL di Azure da un backup con ridondanza geografica
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="1a942-103">Utilizzare PowerShell toorestore un database SQL di Azure da backup</span><span class="sxs-lookup"><span data-stu-id="1a942-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="1a942-104">In questo esempio di script di PowerShell Ripristina un database SQL di Azure da un backup con ridondanza geografica, ripristina un eliminato SQL Azure database tooits più recente backup e ripristini un punto specifico di SQL Azure database tooa nel tempo.</span><span class="sxs-lookup"><span data-stu-id="1a942-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="1a942-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="1a942-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1a942-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1a942-106">Clean up deployment</span></span>

<span data-ttu-id="1a942-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="1a942-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="1a942-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="1a942-108">Script explanation</span></span>

<span data-ttu-id="1a942-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="1a942-109">This script uses hello following commands.</span></span> <span data-ttu-id="1a942-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="1a942-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1a942-111">Comando</span><span class="sxs-lookup"><span data-stu-id="1a942-111">Command</span></span> | <span data-ttu-id="1a942-112">Note</span><span class="sxs-lookup"><span data-stu-id="1a942-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a942-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a942-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="1a942-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="1a942-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="1a942-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="1a942-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="1a942-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="1a942-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="1a942-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1a942-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="1a942-118">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="1a942-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="1a942-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="1a942-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="1a942-120">Ottiene una copia di backup con ridondanza geografica di un database.</span><span class="sxs-lookup"><span data-stu-id="1a942-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="1a942-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1a942-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="1a942-122">Ripristina un database SQL.</span><span class="sxs-lookup"><span data-stu-id="1a942-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="1a942-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1a942-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="1a942-124">Rimuove un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a942-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="1a942-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="1a942-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="1a942-126">Ottiene un database eliminato che è possibile ripristinare.</span><span class="sxs-lookup"><span data-stu-id="1a942-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="1a942-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a942-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1a942-128">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="1a942-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a942-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a942-129">Next steps</span></span>

<span data-ttu-id="1a942-130">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a942-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a942-131">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a942-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
