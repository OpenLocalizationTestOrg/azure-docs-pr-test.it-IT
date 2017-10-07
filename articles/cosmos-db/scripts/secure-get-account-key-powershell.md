---
title: Script di PowerShell-Get account aaaAzure chiavi per cosmosdb | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Ottenere le chiavi di account per cosmosdb
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
ms.openlocfilehash: 9ccee3085dc4fa6507d43e4a220dd5fc32889a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-powershell"></a><span data-ttu-id="12a52-103">Ottenere le chiavi di account per Azure Cosmos DB mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="12a52-103">Get account keys for Azure Cosmos DB using PowerShell</span></span>

<span data-ttu-id="12a52-104">Questo esempio ottiene le chiavi di account per qualsiasi tipo di account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="12a52-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="12a52-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="12a52-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Get hello keys for an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="12a52-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="12a52-106">Clean up deployment</span></span>

<span data-ttu-id="12a52-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="12a52-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="12a52-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="12a52-108">Script explanation</span></span>

<span data-ttu-id="12a52-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="12a52-109">This script uses hello following commands.</span></span> <span data-ttu-id="12a52-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="12a52-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="12a52-111">Comando</span><span class="sxs-lookup"><span data-stu-id="12a52-111">Command</span></span> | <span data-ttu-id="12a52-112">Note</span><span class="sxs-lookup"><span data-stu-id="12a52-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="12a52-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="12a52-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="12a52-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="12a52-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="12a52-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="12a52-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="12a52-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="12a52-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="12a52-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="12a52-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="12a52-118">Richiama un'azione su hello Azure CosmosDB account.</span><span class="sxs-lookup"><span data-stu-id="12a52-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="12a52-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="12a52-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="12a52-120">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="12a52-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="12a52-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12a52-121">Next steps</span></span>

<span data-ttu-id="12a52-122">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="12a52-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="12a52-123">Ulteriori esempi di script di PowerShell di Azure Cosmos DB sono reperibile in hello [gli script di PowerShell di Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="12a52-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
