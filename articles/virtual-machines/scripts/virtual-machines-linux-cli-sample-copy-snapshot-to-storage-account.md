---
title: aaaAzure CLI Script di esempio - snapshot di esportazione o copia come account di archiviazione VHD tooa in area diversa | Documenti Microsoft
description: Esempio di Script Azure CLI - snapshot di esportazione o copia come account di archiviazione tooa disco rigido virtuale nella sottoscrizione uguale o diverso
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
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="a9bb6-103">Esportazione o copia snapshot gestito come account di archiviazione tooa disco rigido virtuale in un paese diverso con CLI</span><span class="sxs-lookup"><span data-stu-id="a9bb6-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="a9bb6-104">Questo script consente di esportare un account di archiviazione snapshot gestito tooa in area diversa.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="a9bb6-105">Innanzitutto genera hello URI SAS dello snapshot hello e Usa quindi toocopy è tooa account di archiviazione in paese diverso.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="a9bb6-106">Utilizzare il backup di toomaintain script dei dischi gestiti nell'area geografica diversa per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a9bb6-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a9bb6-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="a9bb6-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a9bb6-108">Script explanation</span></span>

<span data-ttu-id="a9bb6-109">Questo script Usa i comandi toogenerate seguente URI SAS per un gestito hello snapshot e copie snapshot tooa account di archiviazione utilizzando URI SAS.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="a9bb6-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a9bb6-111">Comando</span><span class="sxs-lookup"><span data-stu-id="a9bb6-111">Command</span></span> | <span data-ttu-id="a9bb6-112">Note</span><span class="sxs-lookup"><span data-stu-id="a9bb6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9bb6-113">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="a9bb6-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="a9bb6-114">Genera l'errore SAS di sola lettura toocopy utilizzati account di archiviazione tooa file disco rigido virtuale sottostante o scaricarlo tooon locale</span><span class="sxs-lookup"><span data-stu-id="a9bb6-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="a9bb6-115">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="a9bb6-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="a9bb6-116">Copia un blob in modo asincrono da un tooanother di account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a9bb6-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9bb6-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9bb6-117">Next steps</span></span>

[<span data-ttu-id="a9bb6-118">Creare un disco gestito da un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="a9bb6-118">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="a9bb6-119">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="a9bb6-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="a9bb6-120">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9bb6-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a9bb6-121">Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9bb6-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
