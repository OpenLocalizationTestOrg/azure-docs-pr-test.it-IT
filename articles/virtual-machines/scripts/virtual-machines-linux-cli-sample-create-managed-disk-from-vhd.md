---
title: aaaAzure CLI Script di esempio - creare un disco gestito da un file di disco rigido virtuale in un account di archiviazione in hello stessa sottoscrizione | Documenti Microsoft
description: 'Azure CLI Script di esempio: creare un disco gestito da un file VHD in un account di archiviazione in hello stessa sottoscrizione'
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="dad31-103">Creare un disco gestito da un file di disco rigido virtuale in un account di archiviazione in hello stessa sottoscrizione con CLI</span><span class="sxs-lookup"><span data-stu-id="dad31-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="dad31-104">Questo script crea un disco gestito da un file VHD in un account di archiviazione in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dad31-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="dad31-105">Utilizzare questo tooimport script un specializzata (non generalizzato/preparata con Sysprep) disco rigido virtuale del sistema operativo toomanaged disco toocreate una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dad31-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="dad31-106">Oppure, tooimport un disco di dati dati toomanaged disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="dad31-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dad31-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="dad31-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="dad31-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="dad31-108">Script explanation</span></span>

<span data-ttu-id="dad31-109">Questo script utilizza seguenti comandi toocreate un disco gestito da un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="dad31-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="dad31-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="dad31-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dad31-111">Comando</span><span class="sxs-lookup"><span data-stu-id="dad31-111">Command</span></span> | <span data-ttu-id="dad31-112">Note</span><span class="sxs-lookup"><span data-stu-id="dad31-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dad31-113">az disk create</span><span class="sxs-lookup"><span data-stu-id="dad31-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="dad31-114">Crea un disco gestito utilizzando l'URI di un disco rigido virtuale in un account di archiviazione in hello stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="dad31-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dad31-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dad31-115">Next steps</span></span>

[<span data-ttu-id="dad31-116">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="dad31-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="dad31-117">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dad31-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dad31-118">Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dad31-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
