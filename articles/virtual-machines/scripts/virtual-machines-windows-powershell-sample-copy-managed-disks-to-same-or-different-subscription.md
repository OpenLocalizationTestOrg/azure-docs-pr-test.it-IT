---
title: Script di PowerShell di esempio - aaaAzure copia (spostare) gestiti toosame dischi o una sottoscrizione diversa | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - toosame dischi gestito di copia (spostare) o una sottoscrizione diversa
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
ms.openlocfilehash: 22e19a47228cbf628bebebd73012b8aa7baf073c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="a9954-103">Copia gestito dischi hello stessa sottoscrizione o diversi con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9954-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="a9954-104">Questo script crea una copia di un disco gestito esistente nel hello stessa sottoscrizione o una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="a9954-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="a9954-105">Hello viene creato nuovo disco in hello stessa area padre hello gestiti disco.</span><span class="sxs-lookup"><span data-stu-id="a9954-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a9954-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a9954-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="a9954-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a9954-107">Script explanation</span></span>

<span data-ttu-id="a9954-108">Questo script Usa la seguente comandi toocreate un nuovo disco gestito nella sottoscrizione di destinazione hello utilizzando hello Id dell'origine hello gestiti disco.</span><span class="sxs-lookup"><span data-stu-id="a9954-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="a9954-109">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="a9954-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a9954-110">Comando</span><span class="sxs-lookup"><span data-stu-id="a9954-110">Command</span></span> | <span data-ttu-id="a9954-111">Note</span><span class="sxs-lookup"><span data-stu-id="a9954-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9954-112">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="a9954-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="a9954-113">Crea la configurazione del disco usata per la creazione del disco.</span><span class="sxs-lookup"><span data-stu-id="a9954-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="a9954-114">Sono incluse risorse hello Id del disco padre hello e il percorso che corrisponde al percorso di hello del disco padre.</span><span class="sxs-lookup"><span data-stu-id="a9954-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="a9954-115">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a9954-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="a9954-116">Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a9954-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a9954-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9954-117">Next steps</span></span>

[<span data-ttu-id="a9954-118">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="a9954-118">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a9954-119">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9954-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a9954-120">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9954-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
