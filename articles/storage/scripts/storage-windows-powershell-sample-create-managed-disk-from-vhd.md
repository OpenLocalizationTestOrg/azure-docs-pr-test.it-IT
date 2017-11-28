---
title: aaaAzure Script di PowerShell di esempio - creare un disco gestito da un file di disco rigido virtuale in un account di archiviazione nella sottoscrizione uguale o diverso | Documenti Microsoft
description: 'Esempio di script di Azure PowerShell: creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un''altra'
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="ed0ed-103">Creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed0ed-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="ed0ed-104">Questo script crea un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="ed0ed-105">Utilizzare questo tooimport script un specializzata (non generalizzato/preparata con Sysprep) disco rigido virtuale del sistema operativo toomanaged disco toocreate una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="ed0ed-106">Inoltre, utilizzarla tooimport un disco di dati dati toomanaged disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="ed0ed-107">Non creare più dischi gestiti identici da un file VHD in poco tempo.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="ed0ed-108">toocreate dischi gestiti da un file vhd, snapshot del blob del file di disco rigido virtuale hello viene creato e quindi i dischi utilizzati toocreate gestito è.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="ed0ed-109">È possibile creare snapshot del blob di un solo in un minuto che causa errori di creazione del disco toothrottling scadenza.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="ed0ed-110">tooavoid questa limitazione, creare un [snapshot gestito dal file di disco rigido virtuale hello](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e quindi utilizzare hello gestiti snapshot toocreate più dischi gestiti nel periodo di tempo breve.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ed0ed-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ed0ed-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="ed0ed-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ed0ed-112">Script explanation</span></span>

<span data-ttu-id="ed0ed-113">Questo script utilizza seguenti comandi toocreate un disco gestito da un disco rigido virtuale in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="ed0ed-114">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ed0ed-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ed0ed-115">Command</span></span> | <span data-ttu-id="ed0ed-116">Note</span><span class="sxs-lookup"><span data-stu-id="ed0ed-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ed0ed-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="ed0ed-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="ed0ed-118">Crea la configurazione del disco usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="ed0ed-119">Tipo di archiviazione, posizione, Id risorsa di hello account di archiviazione in cui è archiviato il padre di hello VHD, VHD URI del VHD principale hello include.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="ed0ed-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="ed0ed-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="ed0ed-121">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed0ed-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ed0ed-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed0ed-122">Next steps</span></span>

[<span data-ttu-id="ed0ed-123">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="ed0ed-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="ed0ed-124">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ed0ed-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ed0ed-125">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed0ed-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
