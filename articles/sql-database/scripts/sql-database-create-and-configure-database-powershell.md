---
title: Esempio di PowerShell - Creare un database SQL di Azure | Microsoft Docs
description: Script di esempio di Azure PowerShell per creare un database SQL di Azure
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
ms.openlocfilehash: 1b6809007e6717b7f8847452b2fa5b38d4ab5ccc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="492e1-103">Usare PowerShell per creare un singolo database SQL di Azure e configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="492e1-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="492e1-104">Questo esempio di script di PowerShell di esempio crea un database SQL di Azure e configura una regola del firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="492e1-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="492e1-105">Dopo aver eseguito correttamente lo script, è possibile accedere al database SQL da tutti i servizi di Azure e dall'indirizzo IP configurato.</span><span class="sxs-lookup"><span data-stu-id="492e1-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="492e1-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="492e1-106">Sample script</span></span>

<span data-ttu-id="492e1-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Creare database SQL")]</span><span class="sxs-lookup"><span data-stu-id="492e1-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="492e1-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="492e1-108">Clean up deployment</span></span>

<span data-ttu-id="492e1-109">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="492e1-109">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="492e1-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="492e1-110">Script explanation</span></span>

<span data-ttu-id="492e1-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="492e1-111">This script uses the following commands.</span></span> <span data-ttu-id="492e1-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="492e1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="492e1-113">Comando</span><span class="sxs-lookup"><span data-stu-id="492e1-113">Command</span></span> | <span data-ttu-id="492e1-114">Note</span><span class="sxs-lookup"><span data-stu-id="492e1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="492e1-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="492e1-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="492e1-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="492e1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="492e1-117">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="492e1-117">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="492e1-118">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="492e1-118">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="492e1-119">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="492e1-119">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="492e1-120">Consente di creare una regola del firewall per consentire l'accesso a tutti i database SQL presenti sul server dall'intervallo di indirizzi IP immesso.</span><span class="sxs-lookup"><span data-stu-id="492e1-120">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="492e1-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="492e1-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="492e1-122">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="492e1-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="492e1-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="492e1-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="492e1-124">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="492e1-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="492e1-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="492e1-125">Next steps</span></span>

<span data-ttu-id="492e1-126">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="492e1-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="492e1-127">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="492e1-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



