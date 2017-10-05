---
title: 'Esempio di script dell''interfaccia della riga di comando di Azure: creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione'
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
ms.openlocfilehash: 5022ca23ac2c2e515a9b80d44b1221f3c05fecb1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="cfa83-103">Creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="cfa83-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="cfa83-104">Questo script crea un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cfa83-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="cfa83-105">Usare questo script per importare un disco rigido virtuale specifico, non generico o preparato con Sysprep, nel disco del sistema operativo gestito per creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cfa83-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="cfa83-106">In alternativa, è possibile usarlo per importare un disco rigido virtuale di dati in un disco di dati gestiti.</span><span class="sxs-lookup"><span data-stu-id="cfa83-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="cfa83-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="cfa83-107">Sample script</span></span>

<span data-ttu-id="cfa83-108">[!code-azurecli[principale](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Creare un disco gestito dal disco rigido virtuale")]</span><span class="sxs-lookup"><span data-stu-id="cfa83-108">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="cfa83-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="cfa83-109">Script explanation</span></span>

<span data-ttu-id="cfa83-110">Questo script usa i comandi seguenti per creare un disco gestito da un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="cfa83-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="cfa83-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="cfa83-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cfa83-112">Comando</span><span class="sxs-lookup"><span data-stu-id="cfa83-112">Command</span></span> | <span data-ttu-id="cfa83-113">Note</span><span class="sxs-lookup"><span data-stu-id="cfa83-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cfa83-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="cfa83-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="cfa83-115">Crea un disco gestito usando l'URI del disco rigido virtuale in un account di archiviazione nella stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cfa83-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cfa83-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cfa83-116">Next steps</span></span>

[<span data-ttu-id="cfa83-117">Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="cfa83-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="cfa83-118">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cfa83-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cfa83-119">Altri esempi di script dell'interfaccia della riga di comando di dischi gestiti e della macchina virtuale aggiuntiva sono reperibili nella [documentazione della macchina virtuale Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfa83-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
