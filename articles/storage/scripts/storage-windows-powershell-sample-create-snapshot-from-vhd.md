---
title: "Esempio di script di Azure PowerShell: Creare uno snapshot da un VHD per ottenere rapidamente più dischi gestiti identici | Microsoft Docs"
description: "Esempio di script di Azure PowerShell: Creare uno snapshot da un VHD per ottenere rapidamente più dischi gestiti identici"
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
ms.openlocfilehash: 8588a33a1f0b4cce0059a40239301587cdc28920
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="feb49-103">Creare uno snapshot da un VHD per ottenere rapidamente più dischi gestiti identici con PowerShell</span><span class="sxs-lookup"><span data-stu-id="feb49-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="feb49-104">Questo script crea uno snapshot da un file VHD in un account di archiviazione nella stessa sottoscrizione o in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="feb49-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="feb49-105">Usare lo script per importare un file VHD specializzato (non generico o preparato con Sysprep) in uno snapshot e quindi usare lo snapshot per creare rapidamente più dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="feb49-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="feb49-106">Usarlo anche per importare un VHD di dati in uno snapshot e quindi usare lo snapshot per creare rapidamente più dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="feb49-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="feb49-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="feb49-107">Sample script</span></span>

<span data-ttu-id="feb49-108">[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Creare uno snapshot da file VHD")]</span><span class="sxs-lookup"><span data-stu-id="feb49-108">[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="feb49-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="feb49-109">Script explanation</span></span>

<span data-ttu-id="feb49-110">Questo script usa i comandi seguenti per creare un disco gestito da un file VHD in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="feb49-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="feb49-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="feb49-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="feb49-112">Comando</span><span class="sxs-lookup"><span data-stu-id="feb49-112">Command</span></span> | <span data-ttu-id="feb49-113">Note</span><span class="sxs-lookup"><span data-stu-id="feb49-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="feb49-114">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="feb49-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="feb49-115">Crea la configurazione usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="feb49-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="feb49-116">Include tipo di archiviazione, posizione, ID risorsa dell'account di archiviazione in cui è archiviato il VHD di origine e URI VHD del file VHD di origine.</span><span class="sxs-lookup"><span data-stu-id="feb49-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="feb49-117">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="feb49-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="feb49-118">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="feb49-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="feb49-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="feb49-119">Next steps</span></span>

[<span data-ttu-id="feb49-120">Creare un disco gestito da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="feb49-120">Create a managed disk from snapshot</span></span>](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="feb49-121">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="feb49-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="feb49-122">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="feb49-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="feb49-123">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="feb49-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>