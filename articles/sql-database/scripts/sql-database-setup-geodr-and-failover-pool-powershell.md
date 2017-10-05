---
title: Esempio di PowerShell - Replica geografica attiva per un database SQL di Azure in pool | Microsoft Docs
description: Esempio di script di Azure PowerShell per configurare la replica geografica attiva per un database SQL di Azure in pool
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: c1a495a8f9960ed60d8589dee9615e075f80c77b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="1b1b2-103">Usare PowerShell per configurare la replica geografica attiva per un database SQL di Azure in pool</span><span class="sxs-lookup"><span data-stu-id="1b1b2-103">Use PowerShell to configure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="1b1b2-104">Questo esempio di script di PowerShell configura la replica geografica attiva per un database SQL di Azure in un pool elastico e ne esegue il failover nella replica secondaria del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="1b1b2-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="1b1b2-105">Sample scripts</span></span>

<span data-ttu-id="1b1b2-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Configurare la replica geografica attiva per pool elastici")]</span><span class="sxs-lookup"><span data-stu-id="1b1b2-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1b1b2-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1b1b2-107">Clean up deployment</span></span>

<span data-ttu-id="1b1b2-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="1b1b2-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="1b1b2-109">Script explanation</span></span>

<span data-ttu-id="1b1b2-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-110">This script uses the following commands.</span></span> <span data-ttu-id="1b1b2-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1b1b2-112">Comando</span><span class="sxs-lookup"><span data-stu-id="1b1b2-112">Command</span></span> | <span data-ttu-id="1b1b2-113">Note</span><span class="sxs-lookup"><span data-stu-id="1b1b2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1b1b2-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1b1b2-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1b1b2-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1b1b2-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="1b1b2-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="1b1b2-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="1b1b2-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="1b1b2-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="1b1b2-119">Crea un pool elastico all'interno di un server logico.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="1b1b2-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1b1b2-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="1b1b2-121">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="1b1b2-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1b1b2-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="1b1b2-123">Aggiorna le proprietà del database o sposta un database all'interno, all'esterno o tra pool elastici.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="1b1b2-124">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="1b1b2-124">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="1b1b2-125">Crea un database secondario per un database esistente e avvia la replica dei dati.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-125">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="1b1b2-126">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1b1b2-126">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="1b1b2-127">Ottiene uno o più database.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-127">Gets one or more databases.</span></span> |
| [<span data-ttu-id="1b1b2-128">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="1b1b2-128">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="1b1b2-129">Un database secondario diventa il database primario per avviare il failover.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-129">Switches a secondary database to be primary in order to initiate failover.</span></span>|
| [<span data-ttu-id="1b1b2-130">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="1b1b2-130">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="1b1b2-131">Ottiene i collegamenti di replica geografica tra un database di SQL Azure e un gruppo di risorse o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-131">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="1b1b2-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1b1b2-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1b1b2-133">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="1b1b2-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1b1b2-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b1b2-134">Next steps</span></span>

<span data-ttu-id="1b1b2-135">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b1b2-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1b1b2-136">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1b1b2-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
