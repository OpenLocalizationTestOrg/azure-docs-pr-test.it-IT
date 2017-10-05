---
title: Esempio di PowerShell - Spostare un database SQL di Azure tra pool elastici SQL | Microsoft Docs
description: Script di esempio di Azure PowerShell per spostare un database SQL tra pool elastici usando PowerShell
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
ms.openlocfilehash: 58f14dc668f25f17e93fcaf30f72b15a46d71484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-create-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="96f09-103">Usare Use PowerShell per creare pool elastici e spostare database tra pool elastici</span><span class="sxs-lookup"><span data-stu-id="96f09-103">Use PowerShell to create elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="96f09-104">Questo esempio di script di PowerShell crea due pool elastici e sposta un database da un pool elastico all'altro, quindi sposta un database all'esterno di un pool elastico in un livello di prestazioni a database singolo.</span><span class="sxs-lookup"><span data-stu-id="96f09-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="96f09-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="96f09-105">Sample script</span></span>

<span data-ttu-id="96f09-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Spostare database tra pool")]</span><span class="sxs-lookup"><span data-stu-id="96f09-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="96f09-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="96f09-107">Clean up deployment</span></span>

<span data-ttu-id="96f09-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="96f09-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="96f09-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="96f09-109">Script explanation</span></span>

<span data-ttu-id="96f09-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="96f09-110">This script uses the following commands.</span></span> <span data-ttu-id="96f09-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="96f09-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="96f09-112">Comando</span><span class="sxs-lookup"><span data-stu-id="96f09-112">Command</span></span> | <span data-ttu-id="96f09-113">Note</span><span class="sxs-lookup"><span data-stu-id="96f09-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="96f09-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="96f09-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="96f09-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="96f09-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="96f09-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="96f09-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="96f09-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="96f09-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="96f09-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="96f09-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="96f09-119">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="96f09-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="96f09-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="96f09-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="96f09-121">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="96f09-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="96f09-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="96f09-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="96f09-123">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="96f09-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="96f09-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="96f09-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="96f09-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="96f09-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="96f09-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96f09-126">Next steps</span></span>

<span data-ttu-id="96f09-127">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96f09-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="96f09-128">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="96f09-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
