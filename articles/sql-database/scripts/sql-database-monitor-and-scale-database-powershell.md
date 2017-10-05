---
title: "Esempio di PowerShell - Monitoraggio e scalabilità di un singolo database SQL di Azure | Microsoft Docs"
description: "Script di esempio di Azure PowerShell per il monitoraggio e la scalabilità di un singolo database SQL di Azure"
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
ms.openlocfilehash: 5d08335f4b1d6c5c6a120cbfb86ab2c62b79bb9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="a94c0-103">Usare PowerShell per monitorare e ridimensionare un singolo database SQL</span><span class="sxs-lookup"><span data-stu-id="a94c0-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="a94c0-104">Questo esempio di script di PowerShell consente di monitorare le metriche delle prestazioni di un database, ne aumenta le prestazioni a un livello superiore e crea una regola di avviso per una delle metriche delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a94c0-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="a94c0-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a94c0-105">Sample script</span></span>

<span data-ttu-id="a94c0-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitorare e ridimensionare database SQL singoli")]</span><span class="sxs-lookup"><span data-stu-id="a94c0-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a94c0-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a94c0-107">Clean up deployment</span></span>

<span data-ttu-id="a94c0-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="a94c0-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a94c0-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a94c0-109">Script explanation</span></span>

<span data-ttu-id="a94c0-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a94c0-110">This script uses the following commands.</span></span> <span data-ttu-id="a94c0-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="a94c0-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a94c0-112">Comando</span><span class="sxs-lookup"><span data-stu-id="a94c0-112">Command</span></span> | <span data-ttu-id="a94c0-113">Note</span><span class="sxs-lookup"><span data-stu-id="a94c0-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="a94c0-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a94c0-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a94c0-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="a94c0-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a94c0-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a94c0-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a94c0-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="a94c0-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a94c0-118">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="a94c0-118">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="a94c0-119">Mostra le informazioni sull'utilizzo delle dimensioni per il database.</span><span class="sxs-lookup"><span data-stu-id="a94c0-119">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="a94c0-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a94c0-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="a94c0-121">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="a94c0-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="a94c0-122">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="a94c0-122">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="a94c0-123">Imposta una regola di avviso per monitorare automaticamente le DTU in futuro.</span><span class="sxs-lookup"><span data-stu-id="a94c0-123">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="a94c0-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a94c0-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a94c0-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="a94c0-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a94c0-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a94c0-126">Next steps</span></span>

<span data-ttu-id="a94c0-127">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a94c0-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a94c0-128">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a94c0-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
