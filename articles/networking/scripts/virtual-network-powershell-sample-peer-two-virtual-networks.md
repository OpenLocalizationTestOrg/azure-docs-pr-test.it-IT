---
title: Esempio di script di Azure PowerShell - Eseguire il peering di due reti virtuali | Microsoft Docs
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
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="8e263-103">Eseguire il peering di due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="8e263-103">Peer two virtual networks</span></span>

<span data-ttu-id="8e263-104">Questo script consente di creare e connettere due reti virtuali nella stessa area usando la rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e263-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="8e263-105">Dopo aver eseguito lo script, verrà creato un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="8e263-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="8e263-106">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="8e263-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8e263-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="8e263-107">Sample script</span></span>

<span data-ttu-id="8e263-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Eseguire il peering di due reti")]</span><span class="sxs-lookup"><span data-stu-id="8e263-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8e263-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="8e263-109">Clean up deployment</span></span> 

<span data-ttu-id="8e263-110">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="8e263-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8e263-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="8e263-111">Script explanation</span></span>

<span data-ttu-id="8e263-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="8e263-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="8e263-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="8e263-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8e263-114">Comando</span><span class="sxs-lookup"><span data-stu-id="8e263-114">Command</span></span> | <span data-ttu-id="8e263-115">Note</span><span class="sxs-lookup"><span data-stu-id="8e263-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8e263-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e263-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8e263-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="8e263-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="8e263-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8e263-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="8e263-119">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e263-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="8e263-120">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="8e263-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="8e263-121">Consente di creare un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="8e263-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="8e263-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e263-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8e263-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="8e263-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8e263-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e263-124">Next steps</span></span>

<span data-ttu-id="8e263-125">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e263-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="8e263-126">Altri esempi di script di PowerShell per la rete sono disponibili nella [documentazione con la panoramica delle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8e263-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>