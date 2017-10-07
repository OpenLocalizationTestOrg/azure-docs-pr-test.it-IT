---
title: aaaAzure CLI Script di esempio - creare una VM Linux con WordPress | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con WordPress
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
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="1c2c4-103">Creare una VM con WordPress</span><span class="sxs-lookup"><span data-stu-id="1c2c4-103">Create a VM with WordPress</span></span>

<span data-ttu-id="1c2c4-104">Questo script crea una macchina virtuale e quindi utilizza script personalizzato estensione tooinstall WordPress di hello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="1c2c4-105">Dopo l'esecuzione dello script hello, è possibile accedere a sito di configurazione di WordPress hello in `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1c2c4-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="1c2c4-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1c2c4-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1c2c4-107">Clean up deployment</span></span> 

<span data-ttu-id="1c2c4-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1c2c4-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="1c2c4-109">Script explanation</span></span>

<span data-ttu-id="1c2c4-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1c2c4-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1c2c4-112">Comando</span><span class="sxs-lookup"><span data-stu-id="1c2c4-112">Command</span></span> | <span data-ttu-id="1c2c4-113">Note</span><span class="sxs-lookup"><span data-stu-id="1c2c4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1c2c4-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1c2c4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1c2c4-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1c2c4-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="1c2c4-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1c2c4-117">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="1c2c4-118">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="1c2c4-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="1c2c4-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="1c2c4-120">Crea un tooallow di regola gruppo di sicurezza rete il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="1c2c4-121">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="1c2c4-122">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="1c2c4-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1c2c4-123">Aggiungere hello estensione Script personalizzata toohello macchina virtuale, che richiama un tooinstall script WordPress.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="1c2c4-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="1c2c4-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1c2c4-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="1c2c4-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1c2c4-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c2c4-126">Next steps</span></span>

<span data-ttu-id="1c2c4-127">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1c2c4-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1c2c4-128">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c2c4-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
