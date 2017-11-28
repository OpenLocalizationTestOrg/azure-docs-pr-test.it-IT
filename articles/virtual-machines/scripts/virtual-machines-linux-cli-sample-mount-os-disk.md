---
title: Esempio di script dell'interfaccia della riga di comando di Azure - montaggio del disco del sistema operativo | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - montaggio del disco del sistema operativo
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b54a94d833644ebfae4c1fac59e4753ab723ced4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="dfd73-103">Risolvere i problemi del disco del sistema operativo della VM</span><span class="sxs-lookup"><span data-stu-id="dfd73-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="dfd73-104">Questo script consente di montare il disco del sistema operativo di una macchina virtuale in cui si è verificato un errore o un problema come disco dati in una seconda macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dfd73-104">This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine.</span></span> <span data-ttu-id="dfd73-105">Può essere utile quando si esegue la risoluzione dei problemi del disco o il ripristino di dati.</span><span class="sxs-lookup"><span data-stu-id="dfd73-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dfd73-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="dfd73-106">Sample script</span></span>

<span data-ttu-id="dfd73-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="dfd73-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="dfd73-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="dfd73-108">Script explanation</span></span>

<span data-ttu-id="dfd73-109">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="dfd73-109">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="dfd73-110">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="dfd73-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dfd73-111">Comando</span><span class="sxs-lookup"><span data-stu-id="dfd73-111">Command</span></span> | <span data-ttu-id="dfd73-112">Note</span><span class="sxs-lookup"><span data-stu-id="dfd73-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dfd73-113">az vm show</span><span class="sxs-lookup"><span data-stu-id="dfd73-113">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="dfd73-114">Recupera un elenco di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dfd73-114">Return a list of virtual machines.</span></span> <span data-ttu-id="dfd73-115">In questo caso, l'opzione di query viene usata per restituire il disco del sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dfd73-115">In this case, the query option is used to return the virtual machine operating system disk.</span></span> <span data-ttu-id="dfd73-116">Questo valore viene quindi aggiunto a un nome di variabile 'uri'.</span><span class="sxs-lookup"><span data-stu-id="dfd73-116">This value is then added to a variable name ‘uri’.</span></span> |
| [<span data-ttu-id="dfd73-117">az vm delete</span><span class="sxs-lookup"><span data-stu-id="dfd73-117">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="dfd73-118">Consente di eliminare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dfd73-118">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="dfd73-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="dfd73-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="dfd73-120">Consente di creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dfd73-120">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="dfd73-121">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="dfd73-121">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="dfd73-122">Collega un disco a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dfd73-122">Attaches a disk to a virtual machine.</span></span> |
| [<span data-ttu-id="dfd73-123">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="dfd73-123">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="dfd73-124">Restituisce gli indirizzi IP di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dfd73-124">Returns the IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dfd73-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dfd73-125">Next steps</span></span>

<span data-ttu-id="dfd73-126">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfd73-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dfd73-127">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfd73-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
