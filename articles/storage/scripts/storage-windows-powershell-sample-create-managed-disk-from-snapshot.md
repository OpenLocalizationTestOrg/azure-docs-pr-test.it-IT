---
title: aaaAzure Script di PowerShell di esempio - creare un disco gestito da uno snapshot | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare un disco gestito da uno snapshot
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="353eb-103">Creare un disco gestito da uno snapshot con PowerShell</span><span class="sxs-lookup"><span data-stu-id="353eb-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="353eb-104">Questo script crea un disco gestito da uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="353eb-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="353eb-105">Usarlo toorestore una macchina virtuale da snapshot di dischi del sistema operativo e dati.</span><span class="sxs-lookup"><span data-stu-id="353eb-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="353eb-106">Creare dischi dati e del sistema operativo gestiti dai rispettivi snapshot e quindi creare una nuova macchina virtuale collegando i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="353eb-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="353eb-107">Collegando i dischi dati creati da snapshot, è anche possibile ripristinare i dischi di dati di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="353eb-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="353eb-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="353eb-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="353eb-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="353eb-109">Script explanation</span></span>

<span data-ttu-id="353eb-110">Questo script utilizza seguenti comandi toocreate un disco gestito da uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="353eb-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="353eb-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="353eb-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="353eb-112">Comando</span><span class="sxs-lookup"><span data-stu-id="353eb-112">Command</span></span> | <span data-ttu-id="353eb-113">Note</span><span class="sxs-lookup"><span data-stu-id="353eb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="353eb-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="353eb-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="353eb-115">Ottiene le proprietà dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="353eb-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="353eb-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="353eb-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="353eb-117">Crea la configurazione del disco usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="353eb-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="353eb-118">Include l'Id dello snapshot padre hello, percorso che corrisponde al percorso di hello del tipo di archiviazione di snapshot e hello padre della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="353eb-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="353eb-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="353eb-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="353eb-120">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="353eb-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="353eb-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="353eb-121">Next steps</span></span>

[<span data-ttu-id="353eb-122">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="353eb-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="353eb-123">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="353eb-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="353eb-124">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="353eb-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
