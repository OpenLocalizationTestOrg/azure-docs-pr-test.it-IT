---
title: Esempio di Script CLI - snapshot (spostare) copia di un disco gestito toosame o altra sottoscrizione con CLI aaaAzure | Documenti Microsoft
description: Esempio di Script Azure CLI - snapshot (spostare) copia di un disco gestito toosame o altra sottoscrizione con CLI
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="f262d-103">Snapshot di copia di un disco gestito toosame o altra sottoscrizione con CLI</span><span class="sxs-lookup"><span data-stu-id="f262d-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="f262d-104">Questo script consente di copiare uno snapshot di un disco gestito toosame o di una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="f262d-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="f262d-105">Utilizzare questo toomove script una sottoscrizione toodifferent snapshot hello snapshot padre hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="f262d-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f262d-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f262d-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="f262d-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f262d-107">Script explanation</span></span>

<span data-ttu-id="f262d-108">Questo script Usa la seguente comandi toocreate uno snapshot nella sottoscrizione di destinazione hello utilizzando hello Id dello snapshot di origine hello.</span><span class="sxs-lookup"><span data-stu-id="f262d-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="f262d-109">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f262d-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f262d-110">Comando</span><span class="sxs-lookup"><span data-stu-id="f262d-110">Command</span></span> | <span data-ttu-id="f262d-111">Note</span><span class="sxs-lookup"><span data-stu-id="f262d-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f262d-112">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="f262d-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="f262d-113">Ottiene tutte le proprietà hello di uno snapshot utilizzando il nome di hello e proprietà gruppo di risorse dello snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="f262d-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="f262d-114">Proprietà ID è utilizzato toocopy hello snapshot toodifferent sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f262d-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="f262d-115">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="f262d-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="f262d-116">Copie di uno snapshot creando uno snapshot diversa sottoscrizione utilizzando hello Id e nome del hello snapshot padre.</span><span class="sxs-lookup"><span data-stu-id="f262d-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="f262d-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f262d-117">Next steps</span></span>

[<span data-ttu-id="f262d-118">Creare una macchina virtuale da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="f262d-118">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="f262d-119">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f262d-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f262d-120">Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f262d-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
