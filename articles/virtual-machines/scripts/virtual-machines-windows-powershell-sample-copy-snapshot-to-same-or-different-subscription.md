---
title: Script di PowerShell - esempio di snapshot di copia (spostare) di un disco gestito toosame o altra sottoscrizione aaaAzure | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - snapshot di copia (spostare) di un disco gestito toosame o altra sottoscrizione
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="5d040-103">Copiare lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d040-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="5d040-104">Questo script crea una copia di uno snapshot nel hello stesso stessa sottoscrizione o una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="5d040-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="5d040-105">Utilizzare questo toomove script una sottoscrizione toodifferent snapshot per la conservazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="5d040-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="5d040-106">L'archiviazione di snapshot in una sottoscrizione diversa impedisce l'eliminazione accidentale di snapshot nella sottoscrizione principale.</span><span class="sxs-lookup"><span data-stu-id="5d040-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5d040-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5d040-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="5d040-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5d040-108">Script explanation</span></span>

<span data-ttu-id="5d040-109">Questo script Usa la seguente comandi toocreate uno snapshot nella sottoscrizione di destinazione hello utilizzando hello Id dello snapshot di origine hello.</span><span class="sxs-lookup"><span data-stu-id="5d040-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="5d040-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="5d040-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5d040-111">Comando</span><span class="sxs-lookup"><span data-stu-id="5d040-111">Command</span></span> | <span data-ttu-id="5d040-112">Note</span><span class="sxs-lookup"><span data-stu-id="5d040-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d040-113">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="5d040-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="5d040-114">Crea la configurazione di snapshot usata per la creazione di snapshot.</span><span class="sxs-lookup"><span data-stu-id="5d040-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="5d040-115">Include hello Id risorsa di snapshot di hello padre e il percorso sia identica a quella snapshot padre hello.</span><span class="sxs-lookup"><span data-stu-id="5d040-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="5d040-116">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="5d040-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="5d040-117">Crea uno snapshot accettando come parametri la configurazione dello snapshot, il nome dello snapshot e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5d040-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="5d040-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d040-118">Next steps</span></span>

[<span data-ttu-id="5d040-119">Creare una macchina virtuale da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="5d040-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="5d040-120">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d040-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5d040-121">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d040-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
