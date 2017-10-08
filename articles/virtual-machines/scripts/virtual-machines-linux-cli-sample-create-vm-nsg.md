---
title: aaaAzure CLI Script di esempio - creare due macchine virtuali con un gruppo interno ed esterno | Documenti Microsoft
description: Script dell'interfaccia della riga di comando Azure di esempio - Creare due macchine virtuali con NSG interno ed esterno
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
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="ef103-103">Proteggere il traffico di rete tra le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ef103-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="ef103-104">Questo script crea due macchine virtuali e protegge tooboth il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="ef103-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="ef103-105">Una macchina virtuale è accessibile su internet di hello e non è un gruppo di sicurezza di rete (gruppo) configurato tooallow traffico sulla porta 22 e la porta 80.</span><span class="sxs-lookup"><span data-stu-id="ef103-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 22 and port 80.</span></span> <span data-ttu-id="ef103-106">Hello seconda macchina virtuale non è accessibile su internet hello e ha tooonly un gruppo configurato consentano il traffico dalla macchina virtuale prima di hello.</span><span class="sxs-lookup"><span data-stu-id="ef103-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ef103-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ef103-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ef103-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ef103-108">Clean up deployment</span></span> 

<span data-ttu-id="ef103-109">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="ef103-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ef103-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ef103-110">Script explanation</span></span>

<span data-ttu-id="ef103-111">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="ef103-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="ef103-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="ef103-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ef103-113">Comando</span><span class="sxs-lookup"><span data-stu-id="ef103-113">Command</span></span> | <span data-ttu-id="ef103-114">Note</span><span class="sxs-lookup"><span data-stu-id="ef103-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ef103-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ef103-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ef103-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ef103-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ef103-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="ef103-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="ef103-118">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef103-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="ef103-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="ef103-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="ef103-120">Consente di creare una subnet.</span><span class="sxs-lookup"><span data-stu-id="ef103-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="ef103-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="ef103-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ef103-122">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="ef103-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="ef103-123">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="ef103-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ef103-124">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="ef103-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="ef103-125">Restituisce informazioni sulla regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="ef103-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="ef103-126">In questo esempio, il nome della regola hello è archiviato in una variabile per l'utilizzo più avanti nello script hello.</span><span class="sxs-lookup"><span data-stu-id="ef103-126">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="ef103-127">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="ef103-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="ef103-128">Consente di aggiornare una regola NSG.</span><span class="sxs-lookup"><span data-stu-id="ef103-128">Updates an NSG rule.</span></span> <span data-ttu-id="ef103-129">In questo esempio, regola di back-end hello è toopass aggiornato al traffico solo dalla subnet front-end di hello.</span><span class="sxs-lookup"><span data-stu-id="ef103-129">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="ef103-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="ef103-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ef103-131">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="ef103-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ef103-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef103-132">Next steps</span></span>

<span data-ttu-id="ef103-133">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ef103-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ef103-134">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef103-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
