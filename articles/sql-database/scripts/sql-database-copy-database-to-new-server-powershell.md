---
title: Esempio di PowerShell - Copiare un database SQL di Azure in un nuovo server | Microsoft Docs
description: Script di esempio di Azure PowerShell per copiare un database SQL in un nuovo server
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="727e3-103">Usare PowerShell per copiare un database SQL in un nuovo server</span><span class="sxs-lookup"><span data-stu-id="727e3-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="727e3-104">Questo esempio di script di PowerShell crea una copia di un database esistente in un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="727e3-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="727e3-105">Copiare un database in un nuovo server</span><span class="sxs-lookup"><span data-stu-id="727e3-105">Copy a database to a new server</span></span>

<span data-ttu-id="727e3-106">[!code-powershell[principale](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copiare un database in un nuovo server")]</span><span class="sxs-lookup"><span data-stu-id="727e3-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="727e3-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="727e3-107">Clean up deployment</span></span>

<span data-ttu-id="727e3-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="727e3-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="727e3-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="727e3-109">Script explanation</span></span>

<span data-ttu-id="727e3-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="727e3-110">This script uses the following commands.</span></span> <span data-ttu-id="727e3-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="727e3-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="727e3-112">Comando</span><span class="sxs-lookup"><span data-stu-id="727e3-112">Command</span></span> | <span data-ttu-id="727e3-113">Note</span><span class="sxs-lookup"><span data-stu-id="727e3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="727e3-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="727e3-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="727e3-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="727e3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="727e3-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="727e3-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="727e3-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="727e3-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="727e3-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="727e3-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="727e3-119">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="727e3-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="727e3-120">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="727e3-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="727e3-121">Crea una copia di un database che al momento usa lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="727e3-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="727e3-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="727e3-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="727e3-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="727e3-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="727e3-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="727e3-124">Next steps</span></span>

<span data-ttu-id="727e3-125">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="727e3-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="727e3-126">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="727e3-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
