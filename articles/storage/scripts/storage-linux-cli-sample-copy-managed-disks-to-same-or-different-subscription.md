---
title: aaaAzure CLI Script di esempio - copia (spostare) gestiti toosame dischi o una sottoscrizione diversa | Documenti Microsoft
description: Azure CLI Script di esempio - toosame dischi gestito di copia (spostare) o una sottoscrizione diversa
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="bd2af-103">Copia di dischi gestiti toosame o altra sottoscrizione con CLI</span><span class="sxs-lookup"><span data-stu-id="bd2af-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="bd2af-104">Questo script viene copiato un toosame disco gestito o una sottoscrizione diversa, ma in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="bd2af-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bd2af-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="bd2af-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="bd2af-106">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="bd2af-106">Script explanation</span></span>

<span data-ttu-id="bd2af-107">Questo script Usa la seguente comandi toocreate un nuovo disco gestito nella sottoscrizione di destinazione hello utilizzando hello Id dell'origine hello gestiti disco.</span><span class="sxs-lookup"><span data-stu-id="bd2af-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="bd2af-108">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="bd2af-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bd2af-109">Comando</span><span class="sxs-lookup"><span data-stu-id="bd2af-109">Command</span></span> | <span data-ttu-id="bd2af-110">Note</span><span class="sxs-lookup"><span data-stu-id="bd2af-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bd2af-111">az disk show</span><span class="sxs-lookup"><span data-stu-id="bd2af-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="bd2af-112">Ottiene tutte le proprietà di hello di un disco gestito utilizzando proprietà di gruppo di risorse e nome hello del disco gestito hello.</span><span class="sxs-lookup"><span data-stu-id="bd2af-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="bd2af-113">Proprietà ID è utilizzato toocopy hello gestito disco toodifferent sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd2af-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="bd2af-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="bd2af-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="bd2af-115">Copia un disco gestito mediante la creazione di un nuovo disco gestito nella sottoscrizione diversi tramite Id e nome padre hello gestiti disco.</span><span class="sxs-lookup"><span data-stu-id="bd2af-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="bd2af-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd2af-116">Next steps</span></span>

[<span data-ttu-id="bd2af-117">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="bd2af-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="bd2af-118">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bd2af-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bd2af-119">Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd2af-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
