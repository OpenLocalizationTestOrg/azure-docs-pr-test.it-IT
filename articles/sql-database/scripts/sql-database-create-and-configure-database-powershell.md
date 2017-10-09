---
title: aaaPowerShell esempio-creazione di un database SQL di Azure | Documenti Microsoft
description: Azure PowerShell esempio script toocreate un database SQL Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="95e1b-103">Utilizzare PowerShell toocreate un singolo database di SQL Azure e configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="95e1b-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="95e1b-104">Questo esempio di script di PowerShell di esempio crea un database SQL di Azure e configura una regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="95e1b-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="95e1b-105">Una volta script hello è stato eseguito correttamente, l'indirizzo IP configurato hello che database SQL sono accessibili da tutti i servizi di Azure e hello.</span><span class="sxs-lookup"><span data-stu-id="95e1b-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="95e1b-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="95e1b-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="95e1b-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="95e1b-107">Clean up deployment</span></span>

<span data-ttu-id="95e1b-108">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="95e1b-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="95e1b-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="95e1b-109">Script explanation</span></span>

<span data-ttu-id="95e1b-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="95e1b-110">This script uses hello following commands.</span></span> <span data-ttu-id="95e1b-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="95e1b-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="95e1b-112">Comando</span><span class="sxs-lookup"><span data-stu-id="95e1b-112">Command</span></span> | <span data-ttu-id="95e1b-113">Note</span><span class="sxs-lookup"><span data-stu-id="95e1b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="95e1b-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="95e1b-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="95e1b-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="95e1b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="95e1b-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="95e1b-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="95e1b-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="95e1b-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="95e1b-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="95e1b-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="95e1b-119">Crea un tooall di accesso tooallow regola firewall SQL database nel server di hello dall'intervallo di indirizzi IP hello immesso.</span><span class="sxs-lookup"><span data-stu-id="95e1b-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="95e1b-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="95e1b-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="95e1b-121">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="95e1b-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="95e1b-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="95e1b-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="95e1b-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="95e1b-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="95e1b-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95e1b-124">Next steps</span></span>

<span data-ttu-id="95e1b-125">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="95e1b-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="95e1b-126">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="95e1b-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



