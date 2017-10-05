---
title: 'Esempio di script dell''interfaccia della riga di comando di Azure: copiare, o spostare, i dischi gestiti nella stessa sottoscrizione o in una sottoscrizione diversa | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: copiare, o spostare, i dischi gestiti nella stessa sottoscrizione o in una sottoscrizione diversa'
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
ms.openlocfilehash: dcf92babf84872ffbbba81127952f8422104c723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="4b43b-103">Copiare i dischi gestiti nella stessa sottoscrizione o in una sottoscrizione diversa con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="4b43b-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="4b43b-104">Questo script consente di copiare un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa ma nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="4b43b-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4b43b-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="4b43b-105">Sample script</span></span>

<span data-ttu-id="4b43b-106">[!code-azurecli[principale](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copiare un disco gestito")]</span><span class="sxs-lookup"><span data-stu-id="4b43b-106">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="4b43b-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="4b43b-107">Script explanation</span></span>

<span data-ttu-id="4b43b-108">Questo script usa i comandi seguenti per creare un nuovo disco gestito nella sottoscrizione di destinazione usando l'ID del disco gestito di origine.</span><span class="sxs-lookup"><span data-stu-id="4b43b-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="4b43b-109">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="4b43b-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4b43b-110">Comando</span><span class="sxs-lookup"><span data-stu-id="4b43b-110">Command</span></span> | <span data-ttu-id="4b43b-111">Note</span><span class="sxs-lookup"><span data-stu-id="4b43b-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4b43b-112">az disk show</span><span class="sxs-lookup"><span data-stu-id="4b43b-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="4b43b-113">Ottiene tutte le proprietà di uno snapshot tramite le proprietà del nome e del gruppo di risorse del disco gestito.</span><span class="sxs-lookup"><span data-stu-id="4b43b-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="4b43b-114">La proprietà ID viene usata per copiare il disco gestito in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="4b43b-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="4b43b-115">az disk create</span><span class="sxs-lookup"><span data-stu-id="4b43b-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="4b43b-116">Consente di copiare un disco gestito creando un nuovo disco gestito in una sottoscrizione diversa tramite l'ID e il nome del disco gestito padre.</span><span class="sxs-lookup"><span data-stu-id="4b43b-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="4b43b-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b43b-117">Next steps</span></span>

[<span data-ttu-id="4b43b-118">Creare una macchina virtuale da un disco gestito</span><span class="sxs-lookup"><span data-stu-id="4b43b-118">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="4b43b-119">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b43b-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4b43b-120">Altri esempi di script dell'interfaccia della riga di comando di dischi gestiti e della macchina virtuale aggiuntiva sono reperibili nella [documentazione della macchina virtuale Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4b43b-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
