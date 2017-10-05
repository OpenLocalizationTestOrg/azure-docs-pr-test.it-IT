---
title: Esempio di PowerShell - Configurare la replica geografica attiva per un singolo database SQL di Azure | Microsoft Docs
description: Script di esempio di Azure PowerShell per configurare la replica geografica attiva per un singolo database SQL di Azure
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
ms.openlocfilehash: b25bc02acda7905cd4c08bbafee1d9b29907d332
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="8efde-103">Usare PowerShell per configurare la replica geografica attiva per un singolo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="8efde-103">Use PowerShell to configure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="8efde-104">Questo esempio di script di PowerShell configura la replica geografica attiva per un singolo database SQL di Azure e ne esegue il failover su una replica secondaria del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="8efde-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="8efde-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="8efde-105">Sample scripts</span></span>

<span data-ttu-id="8efde-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Configurare la replica geografica attiva per database singoli")]</span><span class="sxs-lookup"><span data-stu-id="8efde-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8efde-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="8efde-107">Clean up deployment</span></span>

<span data-ttu-id="8efde-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="8efde-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8efde-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="8efde-109">Script explanation</span></span>

<span data-ttu-id="8efde-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="8efde-110">This script uses the following commands.</span></span> <span data-ttu-id="8efde-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="8efde-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8efde-112">Comando</span><span class="sxs-lookup"><span data-stu-id="8efde-112">Command</span></span> | <span data-ttu-id="8efde-113">Note</span><span class="sxs-lookup"><span data-stu-id="8efde-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8efde-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8efde-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8efde-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="8efde-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8efde-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="8efde-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8efde-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="8efde-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8efde-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="8efde-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="8efde-119">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="8efde-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="8efde-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8efde-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="8efde-121">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="8efde-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="8efde-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8efde-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="8efde-123">Crea un database secondario per un database esistente e avvia la replica dei dati.</span><span class="sxs-lookup"><span data-stu-id="8efde-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="8efde-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8efde-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="8efde-125">Ottiene uno o più database.</span><span class="sxs-lookup"><span data-stu-id="8efde-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="8efde-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8efde-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="8efde-127">Consente di passare un database secondario al ruolo di database primario per avviare il failover.</span><span class="sxs-lookup"><span data-stu-id="8efde-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="8efde-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="8efde-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="8efde-129">Ottiene i collegamenti di replica geografica tra un database di SQL Azure e un gruppo di risorse o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8efde-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="8efde-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8efde-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="8efde-131">Termina la replica dei dati tra un database SQL e il database secondario specificato.</span><span class="sxs-lookup"><span data-stu-id="8efde-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="8efde-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8efde-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8efde-133">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="8efde-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8efde-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8efde-134">Next steps</span></span>

<span data-ttu-id="8efde-135">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8efde-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8efde-136">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8efde-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
