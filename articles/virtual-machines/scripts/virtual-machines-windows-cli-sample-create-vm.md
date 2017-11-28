---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale di Windows Server | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Windows Server
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="7adc6-103">Creare una macchina virtuale con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="7adc6-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="7adc6-104">Questo script crea una macchina virtuale di Azure che esegue Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="7adc6-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="7adc6-105">Dopo l'esecuzione di script hello, è possibile accedere hello virtual machine tramite una connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="7adc6-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7adc6-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7adc6-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7adc6-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="7adc6-107">Clean up deployment</span></span> 

<span data-ttu-id="7adc6-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="7adc6-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="7adc6-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7adc6-109">Script explanation</span></span>

<span data-ttu-id="7adc6-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="7adc6-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="7adc6-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="7adc6-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7adc6-112">Comando</span><span class="sxs-lookup"><span data-stu-id="7adc6-112">Command</span></span> | <span data-ttu-id="7adc6-113">Note</span><span class="sxs-lookup"><span data-stu-id="7adc6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7adc6-114">az group create</span><span class="sxs-lookup"><span data-stu-id="7adc6-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7adc6-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="7adc6-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7adc6-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="7adc6-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="7adc6-117">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="7adc6-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="7adc6-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="7adc6-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="7adc6-119">Consente di creare un indirizzo IP pubblico con un indirizzo IP statico e un nome DNS associato.</span><span class="sxs-lookup"><span data-stu-id="7adc6-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="7adc6-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="7adc6-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="7adc6-121">Crea un gruppo di sicurezza di rete (gruppo), ovvero un limite di sicurezza tra le macchine virtuali internet e hello hello.</span><span class="sxs-lookup"><span data-stu-id="7adc6-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="7adc6-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="7adc6-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="7adc6-123">Crea una scheda di rete virtuale e la collega toohello di rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="7adc6-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="7adc6-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="7adc6-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7adc6-125">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="7adc6-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="7adc6-126">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="7adc6-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="7adc6-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="7adc6-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7adc6-128">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="7adc6-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7adc6-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7adc6-129">Next steps</span></span>

<span data-ttu-id="7adc6-130">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7adc6-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7adc6-131">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7adc6-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
