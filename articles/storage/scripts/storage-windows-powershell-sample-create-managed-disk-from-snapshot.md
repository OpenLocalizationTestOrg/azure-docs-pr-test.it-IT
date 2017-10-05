---
title: Esempio di script di Azure PowerShell - Creare un disco gestito da uno snapshot | Microsoft Docs
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
ms.openlocfilehash: 9105d9dc06eea33b3a4e1eeea7fd793919166c9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="7a35e-103">Creare un disco gestito da uno snapshot con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a35e-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="7a35e-104">Questo script crea un disco gestito da uno snapshot.</span><span class="sxs-lookup"><span data-stu-id="7a35e-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="7a35e-105">Può essere usato per ripristinare una macchina virtuale da snapshot dei dischi del sistema operativo e di dati.</span><span class="sxs-lookup"><span data-stu-id="7a35e-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="7a35e-106">Creare dischi dati e del sistema operativo gestiti dai rispettivi snapshot e quindi creare una nuova macchina virtuale collegando i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="7a35e-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="7a35e-107">Collegando i dischi dati creati da snapshot, è anche possibile ripristinare i dischi di dati di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="7a35e-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7a35e-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7a35e-108">Sample script</span></span>

<span data-ttu-id="7a35e-109">[!code-powershell[principale](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Creare un disco gestito da snapshot")]</span><span class="sxs-lookup"><span data-stu-id="7a35e-109">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="7a35e-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7a35e-110">Script explanation</span></span>

<span data-ttu-id="7a35e-111">Questo script usa i comandi seguenti per creare un disco gestito da snapshot.</span><span class="sxs-lookup"><span data-stu-id="7a35e-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="7a35e-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="7a35e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7a35e-113">Comando</span><span class="sxs-lookup"><span data-stu-id="7a35e-113">Command</span></span> | <span data-ttu-id="7a35e-114">Note</span><span class="sxs-lookup"><span data-stu-id="7a35e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a35e-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="7a35e-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="7a35e-116">Ottiene le proprietà dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="7a35e-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="7a35e-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="7a35e-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="7a35e-118">Crea la configurazione usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="7a35e-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="7a35e-119">Include l'ID risorsa dello snapshot padre, il percorso, che è identico a quello dello snapshot padre, e il tipo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7a35e-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="7a35e-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="7a35e-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="7a35e-121">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7a35e-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="7a35e-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7a35e-122">Next steps</span></span>

[<span data-ttu-id="7a35e-123">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="7a35e-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="7a35e-124">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a35e-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7a35e-125">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a35e-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>