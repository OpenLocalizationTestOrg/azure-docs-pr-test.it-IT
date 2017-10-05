---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM collegando un disco gestito come disco del sistema operativo | Microsoft Docs
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
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="34d09-103">Creare una macchina virtuale usando un disco del sistema operativo gestito esistente con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="34d09-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="34d09-104">Questo script crea una macchina virtuale collegando un disco gestito esistente come disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="34d09-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="34d09-105">Usare questo script negli scenari precedenti:</span><span class="sxs-lookup"><span data-stu-id="34d09-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="34d09-106">Creare una VM da un disco del sistema operativo gestito esistente che è stato copiato da un disco gestito in una sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="34d09-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="34d09-107">Creare una VM da un disco gestito esistente che è stato creato da un file VHD specializzato</span><span class="sxs-lookup"><span data-stu-id="34d09-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="34d09-108">Creare una VM da un disco del sistema operativo gestito esistente che è stato creato da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="34d09-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="34d09-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="34d09-109">Sample script</span></span>

<span data-ttu-id="34d09-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Creare una VM da un disco gestito")]</span><span class="sxs-lookup"><span data-stu-id="34d09-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="34d09-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="34d09-111">Clean up deployment</span></span> 

<span data-ttu-id="34d09-112">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="34d09-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="34d09-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="34d09-113">Script explanation</span></span>

<span data-ttu-id="34d09-114">Questo script usa i comandi seguenti per ottenere le proprietà di un disco gestito, collegare un disco gestito a una nuova VM e creare una VM.</span><span class="sxs-lookup"><span data-stu-id="34d09-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="34d09-115">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="34d09-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="34d09-116">Comando</span><span class="sxs-lookup"><span data-stu-id="34d09-116">Command</span></span> | <span data-ttu-id="34d09-117">Note</span><span class="sxs-lookup"><span data-stu-id="34d09-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="34d09-118">az disk show</span><span class="sxs-lookup"><span data-stu-id="34d09-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="34d09-119">Ottiene le proprietà del disco gestito usando il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="34d09-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="34d09-120">La proprietà Id viene usata per collegare un disco gestito a una nuova VM</span><span class="sxs-lookup"><span data-stu-id="34d09-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="34d09-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="34d09-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="34d09-122">Crea una VM utilizzando un disco del sistema operativo gestito</span><span class="sxs-lookup"><span data-stu-id="34d09-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="34d09-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34d09-123">Next steps</span></span>

<span data-ttu-id="34d09-124">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="34d09-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="34d09-125">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34d09-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
