---
title: database SQL di Azure di esempio-monitor-scala-singolo aaaPowerShell | Documenti Microsoft
description: Nell'esempio di PowerShell Azure script toomonitor e ridimensionare un singolo database di SQL Azure
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="258aa-103">Utilizzare PowerShell toomonitor e ridimensionare un singolo database SQL</span><span class="sxs-lookup"><span data-stu-id="258aa-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="258aa-104">In questo esempio di script di PowerShell monitoraggi hello metriche delle prestazioni di un database, ridimensiona il livello di prestazioni superiore tooa e crea una regola di avviso su una delle metriche delle prestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="258aa-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="258aa-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="258aa-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="258aa-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="258aa-106">Clean up deployment</span></span>

<span data-ttu-id="258aa-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="258aa-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="258aa-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="258aa-108">Script explanation</span></span>

<span data-ttu-id="258aa-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="258aa-109">This script uses hello following commands.</span></span> <span data-ttu-id="258aa-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="258aa-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="258aa-111">Comando</span><span class="sxs-lookup"><span data-stu-id="258aa-111">Command</span></span> | <span data-ttu-id="258aa-112">Note</span><span class="sxs-lookup"><span data-stu-id="258aa-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="258aa-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="258aa-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="258aa-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="258aa-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="258aa-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="258aa-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="258aa-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="258aa-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="258aa-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="258aa-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="258aa-118">Mostra le informazioni di utilizzo di hello dimensioni per database hello.</span><span class="sxs-lookup"><span data-stu-id="258aa-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="258aa-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="258aa-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="258aa-120">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="258aa-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="258aa-121">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="258aa-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="258aa-122">Imposta una regola di avviso tooautomatically monitor Dtu in hello future.</span><span class="sxs-lookup"><span data-stu-id="258aa-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="258aa-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="258aa-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="258aa-124">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="258aa-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="258aa-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="258aa-125">Next steps</span></span>

<span data-ttu-id="258aa-126">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="258aa-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="258aa-127">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="258aa-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
