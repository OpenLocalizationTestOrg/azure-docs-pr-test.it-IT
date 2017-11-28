---
title: 'PowerShell Script: consente di creare un criterio di failover di Azure Cosmos DB aaaAzure | Documenti Microsoft'
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
ms.openlocfilehash: 750127385164cd16837b6e29c506d2b44146a629
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-failover-policy-for-high-availability-using-powershell"></a><span data-ttu-id="3156f-103">Creare un criterio di failover per Azure Cosmos DB per la disponibilità elevata con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3156f-103">Create an Azure Cosmos DB failover policy for high availability using PowerShell</span></span>

<span data-ttu-id="3156f-104">Questo script di PowerShell di esempio crea un criterio di failover per la disponibilità elevata per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3156f-104">This sample PowerShell script creates a failover policy for high availability for Azure Cosmos DB.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="3156f-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="3156f-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/modify-failover-priority/modify-failover-priority.ps1?highlight=36-39,42-47 "Create an Azure Cosmos DB DocumentDB API account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3156f-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="3156f-106">Clean up deployment</span></span>

<span data-ttu-id="3156f-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="3156f-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3156f-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="3156f-108">Script explanation</span></span>

<span data-ttu-id="3156f-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3156f-109">This script uses hello following commands.</span></span> <span data-ttu-id="3156f-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="3156f-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3156f-111">Comando</span><span class="sxs-lookup"><span data-stu-id="3156f-111">Command</span></span> | <span data-ttu-id="3156f-112">Note</span><span class="sxs-lookup"><span data-stu-id="3156f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3156f-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3156f-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="3156f-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="3156f-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3156f-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3156f-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="3156f-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="3156f-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="3156f-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="3156f-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="3156f-118">Richiama un'azione su hello Azure CosmosDB account.</span><span class="sxs-lookup"><span data-stu-id="3156f-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="3156f-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3156f-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="3156f-120">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="3156f-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3156f-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3156f-121">Next steps</span></span>

<span data-ttu-id="3156f-122">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="3156f-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="3156f-123">Ulteriori esempi di script di PowerShell di Azure Cosmos DB sono reperibile in hello [gli script di PowerShell di Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3156f-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
