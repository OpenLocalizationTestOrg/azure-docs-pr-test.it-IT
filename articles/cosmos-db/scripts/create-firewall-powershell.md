---
title: 'Script di Azure PowerShell: creare un firewall per Azure Cosmos DB | Microsoft Docs'
description: 'Esempio di script di Azure PowerShell: creazione di un firewall per Azure Cosmos DB'
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
ms.openlocfilehash: caad9212649dd3dc47ddb21555b5b8496c3d2da1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="590f5-103">Azure Cosmos DB: creare un firewall con PowerShell</span><span class="sxs-lookup"><span data-stu-id="590f5-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="590f5-104">Questo esempio di script di PowerShell consente di creare un firewall per qualsiasi tipo di account API di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="590f5-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="590f5-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="590f5-105">Sample script</span></span>

<span data-ttu-id="590f5-106">[!code-powershell[principale](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Creare un firewall per Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="590f5-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="590f5-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="590f5-107">Clean up deployment</span></span>

<span data-ttu-id="590f5-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="590f5-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="590f5-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="590f5-109">Script explanation</span></span>

<span data-ttu-id="590f5-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="590f5-110">This script uses the following commands.</span></span> <span data-ttu-id="590f5-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="590f5-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="590f5-112">Comando</span><span class="sxs-lookup"><span data-stu-id="590f5-112">Command</span></span> | <span data-ttu-id="590f5-113">Note</span><span class="sxs-lookup"><span data-stu-id="590f5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="590f5-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="590f5-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="590f5-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="590f5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="590f5-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="590f5-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="590f5-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="590f5-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="590f5-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="590f5-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="590f5-119">Modifica l'account del database.</span><span class="sxs-lookup"><span data-stu-id="590f5-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="590f5-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="590f5-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="590f5-121">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="590f5-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="590f5-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="590f5-122">Next steps</span></span>

<span data-ttu-id="590f5-123">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="590f5-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="590f5-124">Altri esempi di script PowerShell di Azure Cosmos DB sono disponibili in [Azure Cosmos DB PowerShell scripts](../powershell-samples.md) (Script di PowerShell per Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="590f5-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>