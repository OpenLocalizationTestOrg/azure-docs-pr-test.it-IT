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
ms.openlocfilehash: 6cc0125c08ccb77d014b4642d702c556fffdc8bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="583de-103">Copiare lo snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="583de-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="583de-104">Questo script consente di copiare uno snapshot di un disco gestito nella stessa sottoscrizione o in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="583de-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="583de-105">Usare questo script per spostare uno snapshot in una sottoscrizione diversa nella stessa area come snapshot padre.</span><span class="sxs-lookup"><span data-stu-id="583de-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="583de-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="583de-106">Sample script</span></span>

<span data-ttu-id="583de-107">[!code-azurecli[principale](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copia snapshot")]</span><span class="sxs-lookup"><span data-stu-id="583de-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="583de-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="583de-108">Script explanation</span></span>

<span data-ttu-id="583de-109">Questo script usa i comandi seguenti per creare uno snapshot nella sottoscrizione di destinazione usando l'ID dello snapshot di origine.</span><span class="sxs-lookup"><span data-stu-id="583de-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="583de-110">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="583de-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="583de-111">Comando</span><span class="sxs-lookup"><span data-stu-id="583de-111">Command</span></span> | <span data-ttu-id="583de-112">Note</span><span class="sxs-lookup"><span data-stu-id="583de-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="583de-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="583de-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="583de-114">Ottiene tutte le proprietà di uno snapshot tramite le proprietà del nome e del gruppo di risorse dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="583de-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="583de-115">La proprietà ID viene usata per copiare lo snapshot in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="583de-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="583de-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="583de-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="583de-117">Consente di copiare uno snapshot creando uno snapshot in una sottoscrizione diversa con l'ID e il nome dello snapshot padre.</span><span class="sxs-lookup"><span data-stu-id="583de-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="583de-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="583de-118">Next steps</span></span>

[<span data-ttu-id="583de-119">Creare una macchina virtuale da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="583de-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="583de-120">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="583de-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="583de-121">Altri esempi di script dell'interfaccia della riga di comando di dischi gestiti e della macchina virtuale aggiuntiva sono reperibili nella [documentazione della macchina virtuale Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="583de-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
