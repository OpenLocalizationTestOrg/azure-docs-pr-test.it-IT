---
title: 'Esempio di PowerShell: gruppo di failover con replica geografica per un database SQL di Azure singolo | Microsoft Docs'
description: Script di esempio di Azure PowerShell per configurare la replica geografica attiva per un database SQL di Azure singolo
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
ms.openlocfilehash: 8db8540d9c4caeb53ea8f34d45d9498496d2b8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="3c1d6-103">Usare PowerShell per configurare un gruppo di failover con replica geografica attiva per un database SQL di Azure singolo</span><span class="sxs-lookup"><span data-stu-id="3c1d6-103">Use PowerShell to configure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="3c1d6-104">Questo esempio di script di PowerShell configura un gruppo di failover con replica geografica attiva per un database SQL di Azure singolo e ne effettua il failover in una replica secondaria del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="3c1d6-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="3c1d6-105">Sample scripts</span></span>

<span data-ttu-id="3c1d6-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Configurare un gruppo di failover per un database singolo")]</span><span class="sxs-lookup"><span data-stu-id="3c1d6-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3c1d6-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="3c1d6-107">Clean up deployment</span></span>

<span data-ttu-id="3c1d6-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3c1d6-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="3c1d6-109">Script explanation</span></span>

<span data-ttu-id="3c1d6-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-110">This script uses the following commands.</span></span> <span data-ttu-id="3c1d6-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3c1d6-112">Comando</span><span class="sxs-lookup"><span data-stu-id="3c1d6-112">Command</span></span> | <span data-ttu-id="3c1d6-113">Note</span><span class="sxs-lookup"><span data-stu-id="3c1d6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3c1d6-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3c1d6-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3c1d6-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3c1d6-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="3c1d6-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="3c1d6-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="3c1d6-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="3c1d6-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="3c1d6-119">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="3c1d6-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="3c1d6-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="3c1d6-121">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="3c1d6-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="3c1d6-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="3c1d6-123">Crea un database secondario per un database esistente e avvia la replica dei dati.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="3c1d6-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="3c1d6-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="3c1d6-125">Ottiene uno o più database.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="3c1d6-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="3c1d6-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="3c1d6-127">Consente di passare un database secondario al ruolo di database primario per avviare il failover.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="3c1d6-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="3c1d6-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="3c1d6-129">Ottiene i collegamenti di replica geografica tra un database di SQL Azure e un gruppo di risorse o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="3c1d6-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="3c1d6-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="3c1d6-131">Termina la replica dei dati tra un database SQL e il database secondario specificato.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="3c1d6-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3c1d6-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3c1d6-133">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="3c1d6-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3c1d6-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c1d6-134">Next steps</span></span>

<span data-ttu-id="3c1d6-135">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3c1d6-136">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3c1d6-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
