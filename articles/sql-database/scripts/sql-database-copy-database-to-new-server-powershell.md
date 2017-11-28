---
title: server di database-nuovo SQL Azure di copia di esempio di aaaPowerShell | Documenti Microsoft
description: Azure PowerShell esempio script toocopy un nuovo server tooa database SQL
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
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="82229-103">Utilizzare PowerShell toocopy un nuovo server tooa database SQL</span><span class="sxs-lookup"><span data-stu-id="82229-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="82229-104">Questo esempio di script di PowerShell crea una copia di un database esistente in un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="82229-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="82229-105">Copiare un nuovo server tooa di database</span><span class="sxs-lookup"><span data-stu-id="82229-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="82229-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="82229-106">Clean up deployment</span></span>

<span data-ttu-id="82229-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="82229-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="82229-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="82229-108">Script explanation</span></span>

<span data-ttu-id="82229-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="82229-109">This script uses hello following commands.</span></span> <span data-ttu-id="82229-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="82229-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="82229-111">Comando</span><span class="sxs-lookup"><span data-stu-id="82229-111">Command</span></span> | <span data-ttu-id="82229-112">Note</span><span class="sxs-lookup"><span data-stu-id="82229-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="82229-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="82229-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="82229-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="82229-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="82229-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="82229-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="82229-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="82229-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="82229-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="82229-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="82229-118">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="82229-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="82229-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="82229-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="82229-120">Crea una copia di un database che utilizza snapshot hello in hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="82229-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="82229-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="82229-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="82229-122">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="82229-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="82229-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82229-123">Next steps</span></span>

<span data-ttu-id="82229-124">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82229-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="82229-125">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="82229-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
