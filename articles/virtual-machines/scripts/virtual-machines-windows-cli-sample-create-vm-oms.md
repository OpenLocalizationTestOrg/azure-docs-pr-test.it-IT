---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale di Windows Server 2016 con OMS monitoraggio | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Windows Server 2016 con il monitoraggio di OMS
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="31f07-103">Monitorare una macchina virtuale con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="31f07-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="31f07-104">Questo script crea una macchina virtuale di Azure, installa l'agente di Operations Management Suite (OMS) hello e registra sistema hello con un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="31f07-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="31f07-105">Dopo l'esecuzione dello script di hello, macchina virtuale hello saranno visibile nella console OMS hello.</span><span class="sxs-lookup"><span data-stu-id="31f07-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="31f07-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="31f07-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="31f07-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="31f07-107">Clean up deployment</span></span> 

<span data-ttu-id="31f07-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="31f07-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="31f07-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="31f07-109">Script explanation</span></span>

<span data-ttu-id="31f07-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="31f07-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="31f07-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="31f07-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="31f07-112">Comando</span><span class="sxs-lookup"><span data-stu-id="31f07-112">Command</span></span> | <span data-ttu-id="31f07-113">Note</span><span class="sxs-lookup"><span data-stu-id="31f07-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="31f07-114">az group create</span><span class="sxs-lookup"><span data-stu-id="31f07-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="31f07-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="31f07-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="31f07-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="31f07-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="31f07-117">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="31f07-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="31f07-118">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="31f07-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="31f07-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="31f07-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="31f07-120">Consente di eseguire un'estensione di VM in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="31f07-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="31f07-121">In questo caso, hello estensione agente Operations Management Suite tooinstall utilizzati hello OMS agente e registrare hello macchina virtuale in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="31f07-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="31f07-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="31f07-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="31f07-123">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="31f07-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="31f07-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31f07-124">Next steps</span></span>

<span data-ttu-id="31f07-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="31f07-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="31f07-126">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31f07-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
