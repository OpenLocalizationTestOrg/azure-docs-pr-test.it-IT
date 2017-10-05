---
title: Script di Azure PowerShell - Creare un criterio di failover per Azure Cosmos DB | Documentazione Microsoft
description: Script di Azure PowerShell di esempio - Creare un criterio di failover per Azure Cosmos DB
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
ms.openlocfilehash: 16da3cd543ccbb7fe346261f91d2e9a3ceaf3a8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-failover-policy-for-high-availability-using-powershell"></a><span data-ttu-id="c951b-103">Creare un criterio di failover per Azure Cosmos DB per la disponibilità elevata con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c951b-103">Create an Azure Cosmos DB failover policy for high availability using PowerShell</span></span>

<span data-ttu-id="c951b-104">Questo script di PowerShell di esempio crea un criterio di failover per la disponibilità elevata per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c951b-104">This sample PowerShell script creates a failover policy for high availability for Azure Cosmos DB.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c951b-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c951b-105">Sample script</span></span>

<span data-ttu-id="c951b-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/modify-failover-priority/modify-failover-priority.ps1?highlight=36-39,42-47 "Creare un account dell'API DocumentDB in Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="c951b-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/modify-failover-priority/modify-failover-priority.ps1?highlight=36-39,42-47 "Create an Azure Cosmos DB DocumentDB API account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c951b-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c951b-107">Clean up deployment</span></span>

<span data-ttu-id="c951b-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="c951b-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c951b-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c951b-109">Script explanation</span></span>

<span data-ttu-id="c951b-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c951b-110">This script uses the following commands.</span></span> <span data-ttu-id="c951b-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c951b-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c951b-112">Comando</span><span class="sxs-lookup"><span data-stu-id="c951b-112">Command</span></span> | <span data-ttu-id="c951b-113">Note</span><span class="sxs-lookup"><span data-stu-id="c951b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c951b-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c951b-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="c951b-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c951b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c951b-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c951b-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="c951b-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="c951b-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c951b-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="c951b-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="c951b-119">Chiama un'azione nell'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c951b-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="c951b-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c951b-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="c951b-121">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="c951b-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c951b-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c951b-122">Next steps</span></span>

<span data-ttu-id="c951b-123">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="c951b-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="c951b-124">Altri esempi di script PowerShell di Azure Cosmos DB sono disponibili in [Azure Cosmos DB PowerShell scripts](../powershell-samples.md) (Script di PowerShell per Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="c951b-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>