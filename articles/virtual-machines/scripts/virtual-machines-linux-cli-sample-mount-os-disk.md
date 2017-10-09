---
title: Esempio di Script CLI - montaggio disco del sistema operativo aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="866f0-103">Risolvere i problemi del disco del sistema operativo della VM</span><span class="sxs-lookup"><span data-stu-id="866f0-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="866f0-104">Questo script Monta disco del sistema operativo di una macchina virtuale non riuscita o problematico hello come dati disco tooa seconda macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="866f0-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="866f0-105">Può essere utile quando si esegue la risoluzione dei problemi del disco o il ripristino di dati.</span><span class="sxs-lookup"><span data-stu-id="866f0-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="866f0-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="866f0-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="866f0-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="866f0-107">Script explanation</span></span>

<span data-ttu-id="866f0-108">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="866f0-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="866f0-109">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="866f0-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="866f0-110">Comando</span><span class="sxs-lookup"><span data-stu-id="866f0-110">Command</span></span> | <span data-ttu-id="866f0-111">Note</span><span class="sxs-lookup"><span data-stu-id="866f0-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="866f0-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="866f0-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="866f0-113">Recupera un elenco di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="866f0-113">Return a list of virtual machines.</span></span> <span data-ttu-id="866f0-114">In questo caso, l'opzione query hello è disco del sistema operativo utilizzato tooreturn hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="866f0-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="866f0-115">Questo valore viene quindi aggiunto tooa. nome della variabile 'uri'.</span><span class="sxs-lookup"><span data-stu-id="866f0-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="866f0-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="866f0-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="866f0-117">Consente di eliminare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="866f0-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="866f0-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="866f0-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="866f0-119">Consente di creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="866f0-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="866f0-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="866f0-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="866f0-121">Collega una macchina virtuale di tooa disco.</span><span class="sxs-lookup"><span data-stu-id="866f0-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="866f0-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="866f0-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="866f0-123">Restituisce hello gli indirizzi IP di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="866f0-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="866f0-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="866f0-124">Next steps</span></span>

<span data-ttu-id="866f0-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="866f0-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="866f0-126">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="866f0-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
