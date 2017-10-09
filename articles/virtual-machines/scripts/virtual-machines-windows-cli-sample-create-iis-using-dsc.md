---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale di Windows Server 2016 con IIS mediante DSC | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Windows Server 2016 con IIS usando DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="6c268-103">Creare una macchina virtuale con IIS usando DSC</span><span class="sxs-lookup"><span data-stu-id="6c268-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="6c268-104">Questo script crea una macchina virtuale e utilizza tooinstall estensione script personalizzato di hello macchina virtuale di Azure DSC e configura IIS.</span><span class="sxs-lookup"><span data-stu-id="6c268-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6c268-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="6c268-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6c268-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="6c268-106">Clean up deployment</span></span> 

<span data-ttu-id="6c268-107">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="6c268-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6c268-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="6c268-108">Script explanation</span></span>

<span data-ttu-id="6c268-109">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="6c268-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6c268-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="6c268-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6c268-111">Comando</span><span class="sxs-lookup"><span data-stu-id="6c268-111">Command</span></span> | <span data-ttu-id="6c268-112">Note</span><span class="sxs-lookup"><span data-stu-id="6c268-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c268-113">az group create</span><span class="sxs-lookup"><span data-stu-id="6c268-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6c268-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="6c268-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c268-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="6c268-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6c268-116">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="6c268-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6c268-117">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="6c268-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="6c268-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="6c268-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6c268-119">Aggiungere la macchina hello estensione Script personalizzata toohello virtuale che richiama un tooinstall script IIS.</span><span class="sxs-lookup"><span data-stu-id="6c268-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="6c268-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="6c268-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="6c268-121">Crea un tooallow di regola gruppo di sicurezza rete il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="6c268-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="6c268-122">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c268-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="6c268-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="6c268-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6c268-124">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="6c268-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c268-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c268-125">Next steps</span></span>

<span data-ttu-id="6c268-126">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c268-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c268-127">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c268-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
