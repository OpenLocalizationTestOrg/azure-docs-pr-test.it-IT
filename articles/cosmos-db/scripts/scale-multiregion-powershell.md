---
title: Script di Azure PowerShell - Replica multiarea per Azure Cosmos DB | Documentazione Microsoft
description: Esempio di script di Azure PowerShell - Replica multiarea per Azure Cosmos DB
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 3a469ba43e6c601f5eb0e13d588cd0bd4a0f8683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="65dba-103">Replicare l'account di database di Azure Cosmos DB in più aree e configurare le priorità di failover mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="65dba-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="65dba-104">Questo esempio replica qualsiasi tipo di database di Azure Cosmos DB in più aree e configura le priorità di failover mediante PoweShell.</span><span class="sxs-lookup"><span data-stu-id="65dba-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="65dba-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="65dba-105">Sample script</span></span>

<span data-ttu-id="65dba-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicare un account Azure Cosmos DB su più aree")]</span><span class="sxs-lookup"><span data-stu-id="65dba-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="65dba-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="65dba-107">Clean up deployment</span></span>

<span data-ttu-id="65dba-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="65dba-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="65dba-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="65dba-109">Script explanation</span></span>

<span data-ttu-id="65dba-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="65dba-110">This script uses the following commands.</span></span> <span data-ttu-id="65dba-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="65dba-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="65dba-112">Comando</span><span class="sxs-lookup"><span data-stu-id="65dba-112">Command</span></span> | <span data-ttu-id="65dba-113">Note</span><span class="sxs-lookup"><span data-stu-id="65dba-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="65dba-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="65dba-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="65dba-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="65dba-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="65dba-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="65dba-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="65dba-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="65dba-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="65dba-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="65dba-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="65dba-119">Modifica l'account del database.</span><span class="sxs-lookup"><span data-stu-id="65dba-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="65dba-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="65dba-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="65dba-121">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="65dba-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="65dba-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65dba-122">Next steps</span></span>

<span data-ttu-id="65dba-123">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="65dba-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="65dba-124">Altri esempi di script PowerShell di Azure Cosmos DB sono disponibili in [Azure Cosmos DB PowerShell scripts](../powershell-samples.md) (Script di PowerShell per Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="65dba-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>