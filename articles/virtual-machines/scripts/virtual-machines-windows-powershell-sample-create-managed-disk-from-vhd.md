---
title: 'Esempio di script di Azure PowerShell: creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un''altra | Microsoft Docs'
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
ms.openlocfilehash: 728def40a3eb132537decbd099fa71f4544c6b87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="79745-103">Creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra con PowerShell</span><span class="sxs-lookup"><span data-stu-id="79745-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="79745-104">Questo script crea un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra.</span><span class="sxs-lookup"><span data-stu-id="79745-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="79745-105">Usare questo script per importare un disco rigido virtuale specializzato (non generico/preparato con Sysprep) nel disco del sistema operativo gestito per creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="79745-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="79745-106">In alternativa, usarlo per importare un disco rigido virtuale di dati in un disco dati gestito.</span><span class="sxs-lookup"><span data-stu-id="79745-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="79745-107">Non creare più dischi gestiti identici da un file VHD in poco tempo.</span><span class="sxs-lookup"><span data-stu-id="79745-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="79745-108">Per creare dischi gestiti da un file VHD, viene creato lo snapshot del BLOB del file VHD e successivamente viene usato per creare dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="79745-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="79745-109">È possibile creare un solo snapshot del BLOB in un minuto perché causa errori di creazione del disco dovuti alla limitazione.</span><span class="sxs-lookup"><span data-stu-id="79745-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="79745-110">Per evitare questa limitazione, creare uno [snapshot gestito dal file VHD](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e quindi usarlo per creare più dischi gestiti in poco tempo.</span><span class="sxs-lookup"><span data-stu-id="79745-110">To avoid this throttling, create a [managed snapshot from the vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="79745-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="79745-111">Sample script</span></span>

<span data-ttu-id="79745-112">[!code-powershell[principale](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Creare un disco gestito dal disco rigido virtuale")]</span><span class="sxs-lookup"><span data-stu-id="79745-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="79745-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="79745-113">Script explanation</span></span>

<span data-ttu-id="79745-114">Questo script usa i comandi seguenti per creare un disco gestito da un file VHD in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="79745-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="79745-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="79745-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="79745-116">Comando</span><span class="sxs-lookup"><span data-stu-id="79745-116">Command</span></span> | <span data-ttu-id="79745-117">Note</span><span class="sxs-lookup"><span data-stu-id="79745-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="79745-118">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="79745-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="79745-119">Crea la configurazione del disco usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="79745-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="79745-120">Include il tipo di archiviazione, la posizione, l'ID risorsa dell'account di archiviazione in cui è archiviato il VHD di origine e l'URI VHD del VHD padre.</span><span class="sxs-lookup"><span data-stu-id="79745-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="79745-121">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="79745-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="79745-122">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="79745-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="79745-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79745-123">Next steps</span></span>

[<span data-ttu-id="79745-124">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="79745-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="79745-125">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="79745-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="79745-126">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79745-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>