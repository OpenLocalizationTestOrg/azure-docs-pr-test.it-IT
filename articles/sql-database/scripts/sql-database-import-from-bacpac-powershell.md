---
title: Esempio di PowerShell - Importare un file BACPAC in un database SQL di Azure | Microsoft Docs
description: Script di esempio di Azure PowerShell per importare un file BACPAC in un database SQL
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
ms.openlocfilehash: 20e1d4c195314d6e828e1dac6afae8be11805b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="2b8d2-103">Usare PowerShell per importare un file BACPAC in un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="2b8d2-103">Use PowerShell to import a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="2b8d2-104">Questo esempio di script di PowerShell importa un database da un file **BACPAC** in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="2b8d2-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2b8d2-105">Sample script</span></span>

<span data-ttu-id="2b8d2-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Creare database SQL")]</span><span class="sxs-lookup"><span data-stu-id="2b8d2-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2b8d2-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2b8d2-107">Clean up deployment</span></span>

<span data-ttu-id="2b8d2-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2b8d2-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2b8d2-109">Script explanation</span></span>

<span data-ttu-id="2b8d2-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-110">This script uses the following commands.</span></span> <span data-ttu-id="2b8d2-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2b8d2-112">Comando</span><span class="sxs-lookup"><span data-stu-id="2b8d2-112">Command</span></span> | <span data-ttu-id="2b8d2-113">Note</span><span class="sxs-lookup"><span data-stu-id="2b8d2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b8d2-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2b8d2-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2b8d2-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2b8d2-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="2b8d2-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="2b8d2-117">Consente di creare un server logico che ospita il database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="2b8d2-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="2b8d2-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="2b8d2-119">Consente di creare una regola del firewall per consentire l'accesso a tutti i database SQL presenti sul server dall'intervallo di indirizzi IP immesso.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="2b8d2-120">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="2b8d2-120">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="2b8d2-121">Importa un file BACPAC e crea un nuovo database nel server.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-121">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="2b8d2-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2b8d2-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2b8d2-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="2b8d2-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b8d2-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b8d2-124">Next steps</span></span>

<span data-ttu-id="2b8d2-125">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2b8d2-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2b8d2-126">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2b8d2-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
