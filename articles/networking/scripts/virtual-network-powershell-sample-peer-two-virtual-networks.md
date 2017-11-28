---
title: Esempio di Script di PowerShell - aaaAzure Peer due reti virtuali | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Eseguire il peering di due reti virtuali
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="49d9c-103">Eseguire il peering di due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="49d9c-103">Peer two virtual networks</span></span>

<span data-ttu-id="49d9c-104">Questo script crea e si connette due reti virtuali in hello hello di trhough area stessa rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="49d9c-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="49d9c-105">Dopo l'esecuzione di script hello, si creerà un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="49d9c-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="49d9c-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="49d9c-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="49d9c-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="49d9c-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="49d9c-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="49d9c-108">Clean up deployment</span></span> 

<span data-ttu-id="49d9c-109">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="49d9c-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="49d9c-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="49d9c-110">Script explanation</span></span>

<span data-ttu-id="49d9c-111">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="49d9c-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="49d9c-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="49d9c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="49d9c-113">Comando</span><span class="sxs-lookup"><span data-stu-id="49d9c-113">Command</span></span> | <span data-ttu-id="49d9c-114">Note</span><span class="sxs-lookup"><span data-stu-id="49d9c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="49d9c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="49d9c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="49d9c-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="49d9c-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="49d9c-117">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="49d9c-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="49d9c-118">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="49d9c-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="49d9c-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="49d9c-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="49d9c-120">Consente di creare un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="49d9c-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="49d9c-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="49d9c-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="49d9c-122">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="49d9c-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="49d9c-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49d9c-123">Next steps</span></span>

<span data-ttu-id="49d9c-124">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="49d9c-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="49d9c-125">Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49d9c-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
