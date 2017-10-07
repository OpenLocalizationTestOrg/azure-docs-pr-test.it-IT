---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale collegando un disco come disco del sistema operativo gestito | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM collegando un disco gestito come disco del sistema operativo
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="f2209-103">Creare una macchina virtuale usando un disco del sistema operativo gestito esistente con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="f2209-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="f2209-104">Questo script crea una macchina virtuale collegando un disco gestito esistente come disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f2209-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="f2209-105">Usare questo script negli scenari precedenti:</span><span class="sxs-lookup"><span data-stu-id="f2209-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="f2209-106">Creare una VM da un disco del sistema operativo gestito esistente che è stato copiato da un disco gestito in una sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="f2209-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="f2209-107">Creare una VM da un disco gestito esistente che è stato creato da un file VHD specializzato</span><span class="sxs-lookup"><span data-stu-id="f2209-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="f2209-108">Creare una VM da un disco del sistema operativo gestito esistente che è stato creato da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="f2209-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f2209-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f2209-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f2209-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f2209-110">Clean up deployment</span></span> 

<span data-ttu-id="f2209-111">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="f2209-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f2209-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f2209-112">Script explanation</span></span>

<span data-ttu-id="f2209-113">Questo script utilizza i seguenti comandi gestiti tooget disco proprietà hello, collegare un disco gestito di tooa nuova macchina virtuale e creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f2209-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="f2209-114">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f2209-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f2209-115">Comando</span><span class="sxs-lookup"><span data-stu-id="f2209-115">Command</span></span> | <span data-ttu-id="f2209-116">Note</span><span class="sxs-lookup"><span data-stu-id="f2209-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f2209-117">az disk show</span><span class="sxs-lookup"><span data-stu-id="f2209-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="f2209-118">Ottiene le proprietà del disco gestito usando il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f2209-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="f2209-119">Proprietà ID è utilizzato tooattach tooa un disco gestito nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f2209-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="f2209-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="f2209-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f2209-121">Crea una VM utilizzando un disco del sistema operativo gestito</span><span class="sxs-lookup"><span data-stu-id="f2209-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="f2209-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2209-122">Next steps</span></span>

<span data-ttu-id="f2209-123">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f2209-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f2209-124">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2209-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
