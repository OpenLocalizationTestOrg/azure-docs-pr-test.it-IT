---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM da uno snapshot | Microsoft Docs
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
ms.openlocfilehash: 6e47c3baebd5b68ec29d55c43dc00ae7665c81f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="6cd0d-103">Creare una macchina virtuale da uno snapshot con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="6cd0d-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="6cd0d-104">Questo script crea una macchina virtuale da uno snapshot di un disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="6cd0d-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6cd0d-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="6cd0d-105">Sample script</span></span>

<span data-ttu-id="6cd0d-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Creare una VM da uno snapshot")]</span><span class="sxs-lookup"><span data-stu-id="6cd0d-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6cd0d-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="6cd0d-107">Clean up deployment</span></span> 

<span data-ttu-id="6cd0d-108">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="6cd0d-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6cd0d-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="6cd0d-109">Script explanation</span></span>

<span data-ttu-id="6cd0d-110">Questo script usa i comandi seguenti per creare un disco gestito, una macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="6cd0d-110">This script uses the following commands to create a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="6cd0d-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="6cd0d-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6cd0d-112">Comando</span><span class="sxs-lookup"><span data-stu-id="6cd0d-112">Command</span></span> | <span data-ttu-id="6cd0d-113">Note</span><span class="sxs-lookup"><span data-stu-id="6cd0d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6cd0d-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="6cd0d-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="6cd0d-115">Ottiene lo snapshot usando il nome dello snapshot e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6cd0d-115">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="6cd0d-116">La proprietà Id dell'oggetto restituito viene usata per creare un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="6cd0d-116">Id property of the returned object is used to create a managed disk.</span></span>  |
| [<span data-ttu-id="6cd0d-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="6cd0d-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="6cd0d-118">Crea dischi gestiti da uno snapshot usando l'ID dello snapshot, il nome del disco, il tipo di archiviazione e la dimensione</span><span class="sxs-lookup"><span data-stu-id="6cd0d-118">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="6cd0d-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="6cd0d-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6cd0d-120">Crea una VM utilizzando un disco del sistema operativo gestito</span><span class="sxs-lookup"><span data-stu-id="6cd0d-120">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6cd0d-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cd0d-121">Next steps</span></span>

<span data-ttu-id="6cd0d-122">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6cd0d-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6cd0d-123">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6cd0d-123">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
