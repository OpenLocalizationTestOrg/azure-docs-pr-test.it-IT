---
title: aaaAzure CLI Script di esempio - creare una VM Linux | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="4107d-103">Creare una macchina virtuale completamente configurata</span><span class="sxs-lookup"><span data-stu-id="4107d-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="4107d-104">Questo script crea una macchina virtuale di Azure con un sistema operativo Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="4107d-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="4107d-105">Dopo l'esecuzione di script hello, è possibile accedere a macchina virtuale hello su SSH.</span><span class="sxs-lookup"><span data-stu-id="4107d-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4107d-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="4107d-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4107d-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="4107d-107">Clean up deployment</span></span> 

<span data-ttu-id="4107d-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="4107d-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4107d-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="4107d-109">Script explanation</span></span>

<span data-ttu-id="4107d-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="4107d-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="4107d-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="4107d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4107d-112">Comando</span><span class="sxs-lookup"><span data-stu-id="4107d-112">Command</span></span> | <span data-ttu-id="4107d-113">Note</span><span class="sxs-lookup"><span data-stu-id="4107d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4107d-114">az group create</span><span class="sxs-lookup"><span data-stu-id="4107d-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4107d-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="4107d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4107d-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="4107d-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="4107d-117">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="4107d-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="4107d-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="4107d-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="4107d-119">Consente di creare un indirizzo IP pubblico con un indirizzo IP statico e un nome DNS associato.</span><span class="sxs-lookup"><span data-stu-id="4107d-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="4107d-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="4107d-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="4107d-121">Crea un gruppo di sicurezza di rete (gruppo), ovvero un limite di sicurezza tra le macchine virtuali internet e hello hello.</span><span class="sxs-lookup"><span data-stu-id="4107d-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="4107d-122">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="4107d-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="4107d-123">Crea un tooallow regola NSG il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="4107d-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="4107d-124">In questo esempio, la porta 22 è aperta al traffico SSH.</span><span class="sxs-lookup"><span data-stu-id="4107d-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="4107d-125">az network nic create</span><span class="sxs-lookup"><span data-stu-id="4107d-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="4107d-126">Crea una scheda di rete virtuale e la collega toohello di rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="4107d-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="4107d-127">az vm create</span><span class="sxs-lookup"><span data-stu-id="4107d-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="4107d-128">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="4107d-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="4107d-129">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="4107d-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="4107d-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="4107d-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="4107d-131">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="4107d-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4107d-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4107d-132">Next steps</span></span>

<span data-ttu-id="4107d-133">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4107d-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4107d-134">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4107d-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
