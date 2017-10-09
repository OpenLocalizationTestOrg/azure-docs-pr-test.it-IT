---
title: database SQL Azure di file di esempio-importazione-bacpac aaaPowerShell | Documenti Microsoft
description: Azure tooimport di script di esempio PowerShell riquadro di un file bacpac in un database SQL
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="dff5d-103">Utilizzare PowerShell tooimport un file bacpac in un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="dff5d-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="dff5d-104">Questo esempio di script di PowerShell importa un database da un file **BACPAC** in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="dff5d-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="dff5d-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="dff5d-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dff5d-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="dff5d-106">Clean up deployment</span></span>

<span data-ttu-id="dff5d-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="dff5d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="dff5d-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="dff5d-108">Script explanation</span></span>

<span data-ttu-id="dff5d-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="dff5d-109">This script uses hello following commands.</span></span> <span data-ttu-id="dff5d-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="dff5d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dff5d-111">Comando</span><span class="sxs-lookup"><span data-stu-id="dff5d-111">Command</span></span> | <span data-ttu-id="dff5d-112">Note</span><span class="sxs-lookup"><span data-stu-id="dff5d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dff5d-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dff5d-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dff5d-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="dff5d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dff5d-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="dff5d-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="dff5d-116">Crea un server logico che gli host hello Database SQL.</span><span class="sxs-lookup"><span data-stu-id="dff5d-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="dff5d-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="dff5d-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="dff5d-118">Crea un tooall di accesso tooallow regola firewall SQL database nel server di hello dall'intervallo di indirizzi IP hello immesso.</span><span class="sxs-lookup"><span data-stu-id="dff5d-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="dff5d-119">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="dff5d-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="dff5d-120">Importa un bacpac file e crea un nuovo database nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="dff5d-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="dff5d-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dff5d-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="dff5d-122">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="dff5d-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dff5d-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dff5d-123">Next steps</span></span>

<span data-ttu-id="dff5d-124">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dff5d-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dff5d-125">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dff5d-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
