---
title: Script di esempio CLI - aaaAzure Peer due reti virtuali | Documenti Microsoft
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
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="341b1-103">Eseguire il peering di due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="341b1-103">Peer two virtual networks</span></span>

<span data-ttu-id="341b1-104">Questo script crea e si connette due reti virtuali in hello hello di trhough area stessa rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="341b1-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="341b1-105">Dopo l'esecuzione di script hello, si creerà un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="341b1-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="341b1-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="341b1-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="341b1-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="341b1-107">Clean up deployment</span></span> 

<span data-ttu-id="341b1-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="341b1-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="341b1-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="341b1-109">Script explanation</span></span>

<span data-ttu-id="341b1-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="341b1-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="341b1-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="341b1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="341b1-112">Comando</span><span class="sxs-lookup"><span data-stu-id="341b1-112">Command</span></span> | <span data-ttu-id="341b1-113">Note</span><span class="sxs-lookup"><span data-stu-id="341b1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="341b1-114">az group create</span><span class="sxs-lookup"><span data-stu-id="341b1-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="341b1-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="341b1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="341b1-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="341b1-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="341b1-117">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="341b1-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="341b1-118">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="341b1-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="341b1-119">Consente di creare un peering tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="341b1-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="341b1-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="341b1-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="341b1-121">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="341b1-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="341b1-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="341b1-122">Next steps</span></span>

<span data-ttu-id="341b1-123">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="341b1-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="341b1-124">Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="341b1-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
