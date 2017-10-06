---
title: aaaAzure CLI Script di esempio - creare un disco gestito da uno snapshot | Documenti Microsoft
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
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="992dc-103">Creare un disco gestito da uno snapshot con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="992dc-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="992dc-104">Questo script crea un disco gestito da uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="992dc-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="992dc-105">Usarlo toorestore una macchina virtuale da snapshot di dischi del sistema operativo e dati.</span><span class="sxs-lookup"><span data-stu-id="992dc-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="992dc-106">Creare dischi dati e del sistema operativo gestiti dai rispettivi snapshot e quindi creare una nuova macchina virtuale collegando i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="992dc-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="992dc-107">Collegando i dischi dati creati da snapshot, è anche possibile ripristinare i dischi di dati di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="992dc-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="992dc-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="992dc-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="992dc-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="992dc-109">Script explanation</span></span>

<span data-ttu-id="992dc-110">Questo script utilizza seguenti comandi toocreate un disco gestito da uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="992dc-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="992dc-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="992dc-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="992dc-112">Comando</span><span class="sxs-lookup"><span data-stu-id="992dc-112">Command</span></span> | <span data-ttu-id="992dc-113">Note</span><span class="sxs-lookup"><span data-stu-id="992dc-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="992dc-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="992dc-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="992dc-115">Ottiene tutte le proprietà hello di uno snapshot utilizzando il nome di hello e proprietà gruppo di risorse dello snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="992dc-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="992dc-116">Proprietà ID è disco gestito toocreate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="992dc-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="992dc-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="992dc-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="992dc-118">Crea un disco gestito mediante l'ID dello snapshot di uno snapshot gestito</span><span class="sxs-lookup"><span data-stu-id="992dc-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="992dc-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="992dc-119">Next steps</span></span>

[<span data-ttu-id="992dc-120">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="992dc-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="992dc-121">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="992dc-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="992dc-122">Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="992dc-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
