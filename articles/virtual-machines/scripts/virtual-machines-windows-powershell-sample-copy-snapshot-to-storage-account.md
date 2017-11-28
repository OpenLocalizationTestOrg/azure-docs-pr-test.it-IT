---
title: Script di PowerShell - esempio di snapshot di esportazione o copia come account di archiviazione VHD tooa in area diversa aaaAzure | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - snapshot di esportazione o copia come account di archiviazione VHD tooa nella stessa area diversa
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
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="10200-103">Esportazione o copia snapshot gestito come account di archiviazione tooa disco rigido virtuale in un paese diverso con PowerShell</span><span class="sxs-lookup"><span data-stu-id="10200-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="10200-104">Questo script consente di esportare un account di archiviazione snapshot gestito tooa in area diversa.</span><span class="sxs-lookup"><span data-stu-id="10200-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="10200-105">Innanzitutto genera hello URI SAS dello snapshot hello e Usa quindi toocopy è tooa account di archiviazione in paese diverso.</span><span class="sxs-lookup"><span data-stu-id="10200-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="10200-106">Utilizzare il backup di toomaintain script dei dischi gestiti nell'area geografica diversa per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="10200-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="10200-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="10200-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="10200-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="10200-108">Script explanation</span></span>

<span data-ttu-id="10200-109">Questo script Usa i comandi toogenerate seguente URI SAS per un gestito hello snapshot e copie snapshot tooa account di archiviazione utilizzando URI SAS.</span><span class="sxs-lookup"><span data-stu-id="10200-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="10200-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="10200-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="10200-111">Comando</span><span class="sxs-lookup"><span data-stu-id="10200-111">Command</span></span> | <span data-ttu-id="10200-112">Note</span><span class="sxs-lookup"><span data-stu-id="10200-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="10200-113">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="10200-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="10200-114">Genera l'errore URI SAS per uno snapshot che è usato toocopy è tooa account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="10200-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="10200-115">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="10200-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="10200-116">Crea un contesto di account di archiviazione utilizzando la chiave e il nome di account hello.</span><span class="sxs-lookup"><span data-stu-id="10200-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="10200-117">In questo contesto può essere operazioni di lettura/scrittura tooperform utilizzati account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="10200-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="10200-118">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="10200-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="10200-119">Copie hello disco rigido virtuale sottostante di un account di archiviazione snapshot tooa</span><span class="sxs-lookup"><span data-stu-id="10200-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="10200-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10200-120">Next steps</span></span>

[<span data-ttu-id="10200-121">Creare un disco gestito da un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="10200-121">Create a managed disk from a VHD</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="10200-122">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="10200-122">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="10200-123">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="10200-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="10200-124">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10200-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
