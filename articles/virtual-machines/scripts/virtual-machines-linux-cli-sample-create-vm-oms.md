---
title: aaaAzure CLI Script di esempio - creare una VM Linux con OMS monitoraggio | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con il monitoraggio di OMS
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
ms.openlocfilehash: 7a329d4f90a20e0e11faa1f5cafd0701574dc440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="fe9b4-103">Monitorare una macchina virtuale con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="fe9b4-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="fe9b4-104">Questo script crea una macchina virtuale di Azure, installa l'agente di Operations Management Suite (OMS) hello e registra sistema hello con un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="fe9b4-105">Dopo l'esecuzione dello script di hello, macchina virtuale hello saranno visibile nella console OMS hello.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fe9b4-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="fe9b4-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fe9b4-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="fe9b4-107">Clean up deployment</span></span> 

<span data-ttu-id="fe9b4-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fe9b4-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="fe9b4-109">Script explanation</span></span>

<span data-ttu-id="fe9b4-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="fe9b4-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fe9b4-112">Comando</span><span class="sxs-lookup"><span data-stu-id="fe9b4-112">Command</span></span> | <span data-ttu-id="fe9b4-113">Note</span><span class="sxs-lookup"><span data-stu-id="fe9b4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fe9b4-114">az group create</span><span class="sxs-lookup"><span data-stu-id="fe9b4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fe9b4-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fe9b4-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="fe9b4-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fe9b4-117">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="fe9b4-118">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="fe9b4-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="fe9b4-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fe9b4-120">Consente di eseguire un'estensione di VM in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="fe9b4-121">In questo caso, hello estensione agente Operations Management Suite tooinstall utilizzati hello OMS agente e registrare hello macchina virtuale in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="fe9b4-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="fe9b4-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fe9b4-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="fe9b4-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fe9b4-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe9b4-124">Next steps</span></span>

<span data-ttu-id="fe9b4-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe9b4-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fe9b4-126">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe9b4-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
