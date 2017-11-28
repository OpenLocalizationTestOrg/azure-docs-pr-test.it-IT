---
title: failover di esempio-replica geografica aaaPowerShell gruppo singolo Database SQL di Azure | Documenti Microsoft
description: Azure tooset di script di esempio di PowerShell di replica geografica attiva per un singolo database di SQL Azure
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
ms.openlocfilehash: 0ea7afb1125b95370811ef7f80cb9eb7391b2443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="2e426-103">Utilizzare PowerShell tooconfigure un gruppo di replica geografica attiva il failover per un singolo database di SQL Azure</span><span class="sxs-lookup"><span data-stu-id="2e426-103">Use PowerShell tooconfigure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="2e426-104">In questo esempio di script di PowerShell consente di configurare un gruppo di replica geografica attiva il failover per un singolo database di SQL Azure e il failover tooa replica secondaria del database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2e426-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="2e426-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2e426-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2e426-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2e426-106">Clean up deployment</span></span>

<span data-ttu-id="2e426-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="2e426-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2e426-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2e426-108">Script explanation</span></span>

<span data-ttu-id="2e426-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2e426-109">This script uses hello following commands.</span></span> <span data-ttu-id="2e426-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="2e426-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2e426-111">Comando</span><span class="sxs-lookup"><span data-stu-id="2e426-111">Command</span></span> | <span data-ttu-id="2e426-112">Note</span><span class="sxs-lookup"><span data-stu-id="2e426-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e426-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2e426-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2e426-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="2e426-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2e426-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="2e426-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="2e426-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="2e426-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="2e426-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="2e426-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="2e426-118">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="2e426-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="2e426-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2e426-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="2e426-120">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="2e426-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="2e426-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="2e426-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="2e426-122">Crea un database secondario per un database esistente e avvia la replica dei dati.</span><span class="sxs-lookup"><span data-stu-id="2e426-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="2e426-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2e426-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="2e426-124">Ottiene uno o più database.</span><span class="sxs-lookup"><span data-stu-id="2e426-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="2e426-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="2e426-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="2e426-126">Attiva un failover primario tooinitiate toobe di database secondario.</span><span class="sxs-lookup"><span data-stu-id="2e426-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="2e426-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="2e426-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="2e426-128">Ottiene i collegamenti di replica geografica hello tra un Database SQL di Azure e un gruppo di risorse o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e426-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="2e426-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="2e426-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="2e426-130">Termina la replica dei dati tra un Database SQL e il database secondario specificato hello.</span><span class="sxs-lookup"><span data-stu-id="2e426-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="2e426-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2e426-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2e426-132">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="2e426-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2e426-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e426-133">Next steps</span></span>

<span data-ttu-id="2e426-134">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e426-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2e426-135">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2e426-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
