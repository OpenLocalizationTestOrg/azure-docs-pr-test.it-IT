---
title: aaaAzure CLI Script di esempio - creazione rapida una VM Linux | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare rapidamente una VM Linux
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
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="2ca6f-103">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2ca6f-103">Create a virtual machine</span></span>

<span data-ttu-id="2ca6f-104">Questo script crea una macchina virtuale di Azure con sistema operativo Ubuntu e le relative risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="2ca6f-105">Dopo l'esecuzione di script hello, è possibile accedere a macchina virtuale hello su SSH.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2ca6f-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2ca6f-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2ca6f-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2ca6f-107">Clean up deployment</span></span> 

<span data-ttu-id="2ca6f-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2ca6f-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2ca6f-109">Script explanation</span></span>

<span data-ttu-id="2ca6f-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2ca6f-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2ca6f-112">Comando</span><span class="sxs-lookup"><span data-stu-id="2ca6f-112">Command</span></span> | <span data-ttu-id="2ca6f-113">Note</span><span class="sxs-lookup"><span data-stu-id="2ca6f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2ca6f-114">az group create</span><span class="sxs-lookup"><span data-stu-id="2ca6f-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2ca6f-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2ca6f-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="2ca6f-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2ca6f-117">Crea macchina virtuale hello e lo connette una scheda di rete toohello, rete virtuale, subnet e il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="2ca6f-118">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="2ca6f-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="2ca6f-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2ca6f-120">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="2ca6f-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2ca6f-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ca6f-121">Next steps</span></span>

<span data-ttu-id="2ca6f-122">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2ca6f-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2ca6f-123">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2ca6f-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
