---
title: 'Esempio di script dell''interfaccia della riga di comando di Azure: snapshot di esportazione/copia come disco rigido virtuale in un account di archiviazione di un''area diversa | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: snapshot di esportazione/copia come disco rigido virtuale in un account di archiviazione nella stessa sottoscrizione o in una sottoscrizione diversa'
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
ms.openlocfilehash: fafb74af5f02f74036c770934c5e33f1b8a5593e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="7e9de-103">Snapshot gestiti di esportazione/copia come disco rigido virtuale in un account di archiviazione di un'area diversa con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="7e9de-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="7e9de-104">Questo script consente di esportare uno snapshot gestito in un account di archiviazione di un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="7e9de-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="7e9de-105">Per prima cosa viene generato l'URI di firma di accesso condiviso dello snapshot, che viene poi usato per copiare lo snapshot in un account di archiviazione di un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="7e9de-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="7e9de-106">Usare questo script per gestire il backup dei dischi gestiti in un'area diversa per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="7e9de-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7e9de-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7e9de-107">Sample script</span></span>

<span data-ttu-id="7e9de-108">[!code-azurecli[principale](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copia snapshot")]</span><span class="sxs-lookup"><span data-stu-id="7e9de-108">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="7e9de-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7e9de-109">Script explanation</span></span>

<span data-ttu-id="7e9de-110">Questo script usa i comandi seguenti per generare l'URI di firma di accesso condiviso per uno snapshot gestito e copia lo snapshot in un account di archiviazione usando tale URI.</span><span class="sxs-lookup"><span data-stu-id="7e9de-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="7e9de-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="7e9de-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7e9de-112">Comando</span><span class="sxs-lookup"><span data-stu-id="7e9de-112">Command</span></span> | <span data-ttu-id="7e9de-113">Note</span><span class="sxs-lookup"><span data-stu-id="7e9de-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7e9de-114">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="7e9de-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="7e9de-115">Genera SAS di sola lettura usati per copiare il file VHD sottostante in un account di archiviazione o scaricarlo in locale</span><span class="sxs-lookup"><span data-stu-id="7e9de-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="7e9de-116">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="7e9de-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="7e9de-117">Copia un BLOB in modo asincrono da un account di archiviazione a un altro</span><span class="sxs-lookup"><span data-stu-id="7e9de-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7e9de-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e9de-118">Next steps</span></span>

[<span data-ttu-id="7e9de-119">Creare un disco gestito da un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="7e9de-119">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="7e9de-120">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="7e9de-120">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="7e9de-121">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7e9de-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7e9de-122">Altri esempi di script dell'interfaccia della riga di comando di dischi gestiti e della macchina virtuale aggiuntiva sono reperibili nella [documentazione della macchina virtuale Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e9de-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
