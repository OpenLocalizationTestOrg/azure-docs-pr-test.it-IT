---
title: pool elastico SQL database SQL di Azure esempio spostamento aaaPowerShell | Documenti Microsoft
description: Azure PowerShell esempio script toomove un database SQL tra il pool elastico con PowerShell
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="9e474-103">Utilizzare i pool elastici toocreate di PowerShell e spostare database tra i pool elastici</span><span class="sxs-lookup"><span data-stu-id="9e474-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="9e474-104">In questo esempio di script di PowerShell consente di creare due pool elastico e sposta un database da un pool elastico in un altro pool elastico e quindi si sposta un database all'esterno di un livello di prestazioni pool elastico tooa singolo database.</span><span class="sxs-lookup"><span data-stu-id="9e474-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="9e474-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9e474-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9e474-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="9e474-106">Clean up deployment</span></span>

<span data-ttu-id="9e474-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="9e474-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="9e474-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9e474-108">Script explanation</span></span>

<span data-ttu-id="9e474-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9e474-109">This script uses hello following commands.</span></span> <span data-ttu-id="9e474-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="9e474-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9e474-111">Comando</span><span class="sxs-lookup"><span data-stu-id="9e474-111">Command</span></span> | <span data-ttu-id="9e474-112">Note</span><span class="sxs-lookup"><span data-stu-id="9e474-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e474-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9e474-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9e474-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="9e474-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9e474-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="9e474-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="9e474-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="9e474-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="9e474-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="9e474-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="9e474-118">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="9e474-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="9e474-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="9e474-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="9e474-120">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="9e474-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="9e474-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="9e474-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="9e474-122">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="9e474-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="9e474-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9e474-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9e474-124">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="9e474-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="9e474-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e474-125">Next steps</span></span>

<span data-ttu-id="9e474-126">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e474-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9e474-127">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9e474-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
