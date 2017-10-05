---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire il peering di due reti virtuali | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire il peering di due reti virtuali
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: a2b8fda288072e2fb0087988bbd68d3e4d9031d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="41379-103">Eseguire il peering di due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="41379-103">Peer two virtual networks</span></span>

<span data-ttu-id="41379-104">Questo script consente di creare e connettere due reti virtuali nella stessa area usando la rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="41379-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="41379-105">Dopo aver eseguito lo script, verrà creato un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="41379-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="41379-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="41379-106">Sample script</span></span>

<span data-ttu-id="41379-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Eseguire il peering di due reti")]</span><span class="sxs-lookup"><span data-stu-id="41379-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="41379-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="41379-108">Clean up deployment</span></span> 

<span data-ttu-id="41379-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="41379-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="41379-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="41379-110">Script explanation</span></span>

<span data-ttu-id="41379-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="41379-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="41379-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="41379-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="41379-113">Comando</span><span class="sxs-lookup"><span data-stu-id="41379-113">Command</span></span> | <span data-ttu-id="41379-114">Note</span><span class="sxs-lookup"><span data-stu-id="41379-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="41379-115">az group create</span><span class="sxs-lookup"><span data-stu-id="41379-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="41379-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="41379-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41379-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="41379-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="41379-118">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="41379-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="41379-119">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="41379-119">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="41379-120">Consente di creare un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="41379-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="41379-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="41379-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="41379-122">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="41379-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41379-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41379-123">Next steps</span></span>

<span data-ttu-id="41379-124">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41379-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="41379-125">Altri esempi di script dell'interfaccia della riga di comando per la rete sono disponibili nella [documentazione con la panoramica delle reti di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="41379-125">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
