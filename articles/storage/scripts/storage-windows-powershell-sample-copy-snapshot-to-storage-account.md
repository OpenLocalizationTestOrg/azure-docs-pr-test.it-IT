---
title: Esempio di script di Azure PowerShell - Esportare/copiare uno snapshot come disco rigido virtuale in un account di archiviazione di un'area diversa | Microsoft Docs
description: Esempio di script di Azure PowerShell - Esportare/copiare uno snapshot come disco rigido virtuale in un account di archiviazione nella stessa area o in un'area diversa
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
ms.openlocfilehash: 80f83f4b66165ddd2bdd0edca2be5d026cb11a9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="c81a1-103">Esportare/copiare snapshot gestiti come disco rigido virtuale in un account di archiviazione di un'area diversa con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c81a1-103">Export/Copy managed snapshots as VHD to a storage account in different region with PowerShell</span></span>

<span data-ttu-id="c81a1-104">Questo script consente di esportare uno snapshot gestito in un account di archiviazione di un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="c81a1-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="c81a1-105">Per prima cosa viene generato l'URI di firma di accesso condiviso dello snapshot, che viene poi usato per copiare lo snapshot in un account di archiviazione di un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="c81a1-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="c81a1-106">Usare questo script per gestire il backup dei dischi gestiti in un'area diversa per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="c81a1-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c81a1-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c81a1-107">Sample script</span></span>

<span data-ttu-id="c81a1-108">[!code-powershell[principale](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copia snapshot")]</span><span class="sxs-lookup"><span data-stu-id="c81a1-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="c81a1-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c81a1-109">Script explanation</span></span>

<span data-ttu-id="c81a1-110">Questo script usa i comandi seguenti per generare l'URI di firma di accesso condiviso per uno snapshot gestito e copia lo snapshot in un account di archiviazione usando tale URI.</span><span class="sxs-lookup"><span data-stu-id="c81a1-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="c81a1-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c81a1-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c81a1-112">Comando</span><span class="sxs-lookup"><span data-stu-id="c81a1-112">Command</span></span> | <span data-ttu-id="c81a1-113">Note</span><span class="sxs-lookup"><span data-stu-id="c81a1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c81a1-114">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="c81a1-114">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="c81a1-115">Genera l'URI di firma di accesso condiviso per uno snapshot, che viene usato per copiarlo in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c81a1-115">Generates SAS URI for a snapshot that is used to copy it to a storage account.</span></span> |
| [<span data-ttu-id="c81a1-116">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="c81a1-116">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="c81a1-117">Crea un contesto per l'account di archiviazione usando nome e chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="c81a1-117">Creates a storage account context using the account name and key.</span></span> <span data-ttu-id="c81a1-118">Questo contesto può essere usato per eseguire operazioni di lettura/scrittura sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c81a1-118">This context can be used to perform read/write operations on the storage account.</span></span> |
| [<span data-ttu-id="c81a1-119">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="c81a1-119">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="c81a1-120">Copia il file VHD sottostante di uno snapshot in un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c81a1-120">Copies the underlying VHD of a snapshot to a storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c81a1-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c81a1-121">Next steps</span></span>

[<span data-ttu-id="c81a1-122">Creare un disco gestito da un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="c81a1-122">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="c81a1-123">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="c81a1-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="c81a1-124">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c81a1-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c81a1-125">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c81a1-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>