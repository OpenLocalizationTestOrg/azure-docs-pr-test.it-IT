---
title: Script di esempio di PowerShell per il monitoraggio e il ridimensionamento di un pool elastico SQL nel database SQL di Azure | Microsoft Docs
description: Script di esempio di Azure PowerShell per il monitoraggio e il ridimensionamento di un pool elastico SQL nel database SQL di Azure
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
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="62f80-103">Usare PowerShell per il monitoraggio e il ridimensionamento di un pool elastico SQL nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="62f80-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="62f80-104">Questo script di esempio PowerShell consente di monitorare la metrica delle prestazioni di un pool elastico, ne aumenta le prestazioni a un livello superiore e crea una regola di avviso per la metrica di una delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="62f80-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="62f80-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="62f80-105">Sample script</span></span>

<span data-ttu-id="62f80-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitorare e ridimensionare database SQL singoli")]</span><span class="sxs-lookup"><span data-stu-id="62f80-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="62f80-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="62f80-107">Clean up deployment</span></span>

<span data-ttu-id="62f80-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="62f80-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="62f80-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="62f80-109">Script explanation</span></span>

<span data-ttu-id="62f80-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="62f80-110">This script uses the following commands.</span></span> <span data-ttu-id="62f80-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="62f80-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="62f80-112">Comando</span><span class="sxs-lookup"><span data-stu-id="62f80-112">Command</span></span> | <span data-ttu-id="62f80-113">Note</span><span class="sxs-lookup"><span data-stu-id="62f80-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="62f80-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="62f80-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="62f80-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="62f80-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="62f80-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="62f80-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="62f80-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="62f80-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="62f80-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="62f80-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="62f80-119">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="62f80-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="62f80-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="62f80-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="62f80-121">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="62f80-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="62f80-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="62f80-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="62f80-123">Mostra le informazioni sull'utilizzo delle dimensioni per il database.</span><span class="sxs-lookup"><span data-stu-id="62f80-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="62f80-124">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="62f80-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="62f80-125">Aggiunge o aggiorna una regola di avviso basata su metriche.</span><span class="sxs-lookup"><span data-stu-id="62f80-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="62f80-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="62f80-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="62f80-127">Aggiorna le proprietà dei pool elastici.</span><span class="sxs-lookup"><span data-stu-id="62f80-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="62f80-128">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="62f80-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="62f80-129">Imposta una regola di avviso per monitorare automaticamente le DTU in futuro.</span><span class="sxs-lookup"><span data-stu-id="62f80-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="62f80-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="62f80-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="62f80-131">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="62f80-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="62f80-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62f80-132">Next steps</span></span>

<span data-ttu-id="62f80-133">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62f80-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="62f80-134">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="62f80-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
