---
title: aaaAzure CLI Script di esempio - installare IIS | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Installare IIS
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="1902f-103">Creare rapidamente una macchina virtuale con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="1902f-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="1902f-104">Questo script crea una macchina virtuale di Azure che esegue Windows Server 2016 e utilizza l'estensione Script personalizzata della macchina virtuale Azure di hello tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="1902f-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="1902f-105">Dopo l'esecuzione di script hello, è possibile accedere il sito Web IIS predefinito hello in indirizzo IP pubblico hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1902f-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1902f-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="1902f-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1902f-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1902f-107">Clean up deployment</span></span> 

<span data-ttu-id="1902f-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="1902f-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="1902f-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="1902f-109">Script explanation</span></span>

<span data-ttu-id="1902f-110">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="1902f-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1902f-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="1902f-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1902f-112">Comando</span><span class="sxs-lookup"><span data-stu-id="1902f-112">Command</span></span> | <span data-ttu-id="1902f-113">Note</span><span class="sxs-lookup"><span data-stu-id="1902f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1902f-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1902f-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1902f-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="1902f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1902f-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="1902f-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1902f-117">Crea macchina virtuale hello e lo connette una scheda di rete toohello, rete virtuale, subnet e il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="1902f-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="1902f-118">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="1902f-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="1902f-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="1902f-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="1902f-120">Crea un tooallow di regola gruppo di sicurezza rete il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1902f-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="1902f-121">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="1902f-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="1902f-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="1902f-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1902f-123">Aggiunge e viene eseguito un tooa di estensione della macchina virtuale macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1902f-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="1902f-124">In questo esempio, un'estensione personalizzata hello è tooinstall utilizzato IIS.</span><span class="sxs-lookup"><span data-stu-id="1902f-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="1902f-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="1902f-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1902f-126">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="1902f-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1902f-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1902f-127">Next steps</span></span>

<span data-ttu-id="1902f-128">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1902f-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1902f-129">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1902f-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
