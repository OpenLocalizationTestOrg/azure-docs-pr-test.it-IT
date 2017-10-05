---
title: 'Esempio di script dell''interfaccia della riga di comando di Azure: creare un disco gestito da uno snapshot | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: creare un disco gestito da uno snapshot'
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 030fa06bc5819443dac5832172a93c2dca28d1ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="cc1f1-103">Creare un disco gestito da uno snapshot con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="cc1f1-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="cc1f1-104">Questo script crea un disco gestito da uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="cc1f1-105">Può essere usato per ripristinare una macchina virtuale da snapshot dei dischi del sistema operativo e di dati.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="cc1f1-106">Creare dischi dati e del sistema operativo gestiti dai rispettivi snapshot e quindi creare una nuova macchina virtuale collegando i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="cc1f1-107">Collegando i dischi dati creati da snapshot, è anche possibile ripristinare i dischi di dati di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="cc1f1-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="cc1f1-108">Sample script</span></span>

<span data-ttu-id="cc1f1-109">[!code-azurecli[principale](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Creare un disco gestito da snapshot")]</span><span class="sxs-lookup"><span data-stu-id="cc1f1-109">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="cc1f1-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="cc1f1-110">Script explanation</span></span>

<span data-ttu-id="cc1f1-111">Questo script usa i comandi seguenti per creare un disco gestito da snapshot.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="cc1f1-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cc1f1-113">Comando</span><span class="sxs-lookup"><span data-stu-id="cc1f1-113">Command</span></span> | <span data-ttu-id="cc1f1-114">Note</span><span class="sxs-lookup"><span data-stu-id="cc1f1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cc1f1-115">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="cc1f1-115">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="cc1f1-116">Ottiene tutte le proprietà di uno snapshot tramite le proprietà del nome e del gruppo di risorse dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-116">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="cc1f1-117">La proprietà ID viene usata per creare un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="cc1f1-117">Id property is used to create managed disk.</span></span>  |
| [<span data-ttu-id="cc1f1-118">az disk create</span><span class="sxs-lookup"><span data-stu-id="cc1f1-118">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="cc1f1-119">Crea un disco gestito mediante l'ID dello snapshot di uno snapshot gestito</span><span class="sxs-lookup"><span data-stu-id="cc1f1-119">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cc1f1-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc1f1-120">Next steps</span></span>

[<span data-ttu-id="cc1f1-121">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="cc1f1-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="cc1f1-122">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cc1f1-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cc1f1-123">Altri esempi di script dell'interfaccia della riga di comando di dischi gestiti e della macchina virtuale aggiuntiva sono reperibili nella [documentazione della macchina virtuale Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc1f1-123">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
