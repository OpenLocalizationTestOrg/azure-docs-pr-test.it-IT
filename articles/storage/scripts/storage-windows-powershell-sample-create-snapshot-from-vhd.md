---
title: "aaaAzure Script di PowerShell di esempio - creare uno snapshot da un disco rigido virtuale toocreate più dischi gestiti identici nel breve periodo di tempo | Documenti Microsoft"
description: "Script di Azure PowerShell di esempio: creare uno snapshot da un disco rigido virtuale toocreate più dischi gestiti identici nel breve periodo di tempo"
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
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="aaffa-103">Creare uno snapshot da un disco rigido virtuale toocreate più dischi gestiti identici nel breve periodo di tempo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaffa-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="aaffa-104">Questo script crea uno snapshot da un file VHD in un account di archiviazione nella stessa sottoscrizione o in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="aaffa-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="aaffa-105">Usare questo tooimport script uno snapshot tooa specializzato del disco rigido virtuale (non generalizzato/preparata con Sysprep) e quindi hello snapshot toocreate più dischi gestiti identici nel breve periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="aaffa-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="aaffa-106">Utilizzare inoltre uno snapshot dei dati dei dischi rigidi Virtuali tooa tooimport e quindi utilizzare più dischi gestiti hello snapshot toocreate nel breve periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="aaffa-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="aaffa-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="aaffa-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="aaffa-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="aaffa-108">Script explanation</span></span>

<span data-ttu-id="aaffa-109">Questo script utilizza seguenti comandi toocreate un disco gestito da un disco rigido virtuale in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="aaffa-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="aaffa-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="aaffa-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="aaffa-111">Comando</span><span class="sxs-lookup"><span data-stu-id="aaffa-111">Command</span></span> | <span data-ttu-id="aaffa-112">Note</span><span class="sxs-lookup"><span data-stu-id="aaffa-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aaffa-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="aaffa-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="aaffa-114">Crea la configurazione del disco usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="aaffa-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="aaffa-115">Include il tipo di archiviazione, percorso, Id risorsa di archiviazione VHD padre hello account di archiviazione di hello e VHD URI del VHD principale hello.</span><span class="sxs-lookup"><span data-stu-id="aaffa-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="aaffa-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="aaffa-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="aaffa-117">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="aaffa-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aaffa-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aaffa-118">Next steps</span></span>

[<span data-ttu-id="aaffa-119">Creare un disco gestito da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="aaffa-119">Create a managed disk from snapshot</span></span>](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="aaffa-120">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="aaffa-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="aaffa-121">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aaffa-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="aaffa-122">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aaffa-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
