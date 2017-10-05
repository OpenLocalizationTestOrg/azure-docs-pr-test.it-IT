---
title: 'Esempio di script dell''interfaccia della riga di comando di Azure: copiare, o spostare, lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa con l''interfaccia della riga di comando | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: copiare, o spostare, lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa con l''interfaccia della riga di comando'
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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="f7d21-103">Copiare lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="f7d21-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="f7d21-104">Questo script consente di copiare uno snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="f7d21-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="f7d21-105">Usare questo script per spostare uno snapshot in una sottoscrizione diversa nella stessa area come snapshot padre.</span><span class="sxs-lookup"><span data-stu-id="f7d21-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f7d21-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f7d21-106">Sample script</span></span>

<span data-ttu-id="f7d21-107">[!code-azurecli[principale](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copia snapshot")]</span><span class="sxs-lookup"><span data-stu-id="f7d21-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="f7d21-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f7d21-108">Script explanation</span></span>

<span data-ttu-id="f7d21-109">Questo script usa i comandi seguenti per creare uno snapshot nella sottoscrizione di destinazione usando l'ID dello snapshot di origine.</span><span class="sxs-lookup"><span data-stu-id="f7d21-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="f7d21-110">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="f7d21-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f7d21-111">Comando</span><span class="sxs-lookup"><span data-stu-id="f7d21-111">Command</span></span> | <span data-ttu-id="f7d21-112">Note</span><span class="sxs-lookup"><span data-stu-id="f7d21-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f7d21-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="f7d21-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="f7d21-114">Ottiene tutte le proprietà di uno snapshot tramite le proprietà del nome e del gruppo di risorse dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="f7d21-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="f7d21-115">La proprietà ID viene usata per copiare lo snapshot in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="f7d21-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="f7d21-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="f7d21-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="f7d21-117">Consente di copiare uno snapshot creando uno snapshot in una sottoscrizione diversa con l'ID e il nome dello snapshot padre.</span><span class="sxs-lookup"><span data-stu-id="f7d21-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="f7d21-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7d21-118">Next steps</span></span>

[<span data-ttu-id="f7d21-119">Creare una macchina virtuale da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="f7d21-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="f7d21-120">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f7d21-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f7d21-121">Altri esempi di script dell'interfaccia della riga di comando di dischi gestiti e della macchina virtuale aggiuntiva sono reperibili nella [documentazione della macchina virtuale Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7d21-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
