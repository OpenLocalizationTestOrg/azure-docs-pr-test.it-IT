---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale da uno snapshot | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM da uno snapshot
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="9b9d7-103">Creare una macchina virtuale da uno snapshot con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="9b9d7-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="9b9d7-104">Questo script crea una macchina virtuale da uno snapshot di un disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9b9d7-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9b9d7-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9b9d7-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9b9d7-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="9b9d7-106">Clean up deployment</span></span> 

<span data-ttu-id="9b9d7-107">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="9b9d7-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9b9d7-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9b9d7-108">Script explanation</span></span>

<span data-ttu-id="9b9d7-109">Questo script utilizza i seguenti comandi toocreate un disco gestito, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="9b9d7-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="9b9d7-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="9b9d7-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9b9d7-111">Comando</span><span class="sxs-lookup"><span data-stu-id="9b9d7-111">Command</span></span> | <span data-ttu-id="9b9d7-112">Note</span><span class="sxs-lookup"><span data-stu-id="9b9d7-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9b9d7-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="9b9d7-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="9b9d7-114">Ottiene lo snapshot usando il nome dello snapshot e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9b9d7-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="9b9d7-115">Proprietà ID di oggetto restituito hello è toocreate usato un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="9b9d7-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="9b9d7-116">az disk create</span><span class="sxs-lookup"><span data-stu-id="9b9d7-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="9b9d7-117">Crea dischi gestiti da uno snapshot usando l'ID dello snapshot, il nome del disco, il tipo di archiviazione e la dimensione</span><span class="sxs-lookup"><span data-stu-id="9b9d7-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="9b9d7-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="9b9d7-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9b9d7-119">Crea una VM utilizzando un disco del sistema operativo gestito</span><span class="sxs-lookup"><span data-stu-id="9b9d7-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9b9d7-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b9d7-120">Next steps</span></span>

<span data-ttu-id="9b9d7-121">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b9d7-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9b9d7-122">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b9d7-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
