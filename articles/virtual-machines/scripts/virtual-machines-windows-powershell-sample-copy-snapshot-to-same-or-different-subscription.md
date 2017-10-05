---
title: 'Esempio di script di Azure PowerShell: copiare, o spostare, lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa | Microsoft Docs'
description: 'Esempio di script di Azure PowerShell: copiare, o spostare, lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa'
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
ms.openlocfilehash: f7b4869669a2c5e840f9bd384dcd6d6096ba58e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="48765-103">Copiare lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa con PowerShell</span><span class="sxs-lookup"><span data-stu-id="48765-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="48765-104">Questo script crea una copia di uno snapshot nella stessa sottoscrizione stessa o in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="48765-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="48765-105">Usare questo script per spostare uno snapshot in un'altra sottoscrizione per la conservazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="48765-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="48765-106">L'archiviazione di snapshot in una sottoscrizione diversa impedisce l'eliminazione accidentale di snapshot nella sottoscrizione principale.</span><span class="sxs-lookup"><span data-stu-id="48765-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="48765-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="48765-107">Sample script</span></span>

<span data-ttu-id="48765-108">[!code-powershell[principale](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copia snapshot")]</span><span class="sxs-lookup"><span data-stu-id="48765-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="48765-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="48765-109">Script explanation</span></span>

<span data-ttu-id="48765-110">Questo script usa i comandi seguenti per creare uno snapshot nella sottoscrizione di destinazione usando l'ID dello snapshot di origine.</span><span class="sxs-lookup"><span data-stu-id="48765-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="48765-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="48765-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="48765-112">Comando</span><span class="sxs-lookup"><span data-stu-id="48765-112">Command</span></span> | <span data-ttu-id="48765-113">Note</span><span class="sxs-lookup"><span data-stu-id="48765-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="48765-114">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="48765-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="48765-115">Crea la configurazione di snapshot usata per la creazione di snapshot.</span><span class="sxs-lookup"><span data-stu-id="48765-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="48765-116">Include l'ID risorsa dello snapshot padre e il percorso che è identico a quello dello snapshot padre.</span><span class="sxs-lookup"><span data-stu-id="48765-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="48765-117">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="48765-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="48765-118">Crea uno snapshot accettando come parametri la configurazione dello snapshot, il nome dello snapshot e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="48765-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="48765-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48765-119">Next steps</span></span>

[<span data-ttu-id="48765-120">Creare una macchina virtuale da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="48765-120">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="48765-121">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="48765-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="48765-122">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48765-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>