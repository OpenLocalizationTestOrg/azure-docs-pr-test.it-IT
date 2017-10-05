---
title: Esempio di script di Azure PowerShell - Copiare, o spostare, i dischi gestiti nella stessa sottoscrizione o in una sottoscrizione diversa | Microsoft Docs
description: Esempio di script di Azure PowerShell - Copiare, o spostare, i dischi gestiti nella stessa sottoscrizione o in una sottoscrizione diversa
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 75beb35dc19fa530d9b2c19aed6040f74afafbc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="copy-managed-disks-in-the-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="70391-103">Copiare dischi gestiti nella stessa sottoscrizione o in una sottoscrizione diversa con PowerShell</span><span class="sxs-lookup"><span data-stu-id="70391-103">Copy managed disks in the same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="70391-104">Questo script crea una copia di un disco gestito esistente nella stessa sottoscrizione o in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="70391-104">This script creates a copy of an existing managed disk in the same subscription or different subscription.</span></span> <span data-ttu-id="70391-105">Il nuovo disco viene creato nella stessa area del disco gestito padre.</span><span class="sxs-lookup"><span data-stu-id="70391-105">The new disk is created in the same region as the parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="70391-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="70391-106">Sample script</span></span>

<span data-ttu-id="70391-107">[!code-powershell[principale](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copiare un disco gestito")]</span><span class="sxs-lookup"><span data-stu-id="70391-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="70391-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="70391-108">Script explanation</span></span>

<span data-ttu-id="70391-109">Questo script usa i comandi seguenti per creare un nuovo disco gestito nella sottoscrizione di destinazione usando l'ID del disco gestito di origine.</span><span class="sxs-lookup"><span data-stu-id="70391-109">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="70391-110">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="70391-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="70391-111">Comando</span><span class="sxs-lookup"><span data-stu-id="70391-111">Command</span></span> | <span data-ttu-id="70391-112">Note</span><span class="sxs-lookup"><span data-stu-id="70391-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="70391-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="70391-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="70391-114">Crea la configurazione usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="70391-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="70391-115">Include l'ID risorsa del disco padre e il percorso che è identico a quello del disco padre.</span><span class="sxs-lookup"><span data-stu-id="70391-115">It includes the resource Id of the parent disk and location that is same as the location of parent disk.</span></span>  |
| [<span data-ttu-id="70391-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="70391-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="70391-117">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="70391-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="70391-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70391-118">Next steps</span></span>

[<span data-ttu-id="70391-119">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="70391-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="70391-120">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="70391-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="70391-121">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70391-121">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>