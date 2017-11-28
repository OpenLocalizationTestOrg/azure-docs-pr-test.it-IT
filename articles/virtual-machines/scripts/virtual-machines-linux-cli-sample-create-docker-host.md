---
title: aaaAzure CLI Script di esempio - creare un host Docker | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un host Docker
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="581ad-103">Creare una VM con Docker</span><span class="sxs-lookup"><span data-stu-id="581ad-103">Create a VM with Docker</span></span>

<span data-ttu-id="581ad-104">Questo script crea una macchina virtuale con Docker abilitato e avvia un contenitore Docker che esegue NGINX.</span><span class="sxs-lookup"><span data-stu-id="581ad-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="581ad-105">Dopo l'esecuzione di script hello, è possibile accedere tramite hello FQDN di hello macchina virtuale di Azure con i server web NGINX di hello.</span><span class="sxs-lookup"><span data-stu-id="581ad-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="581ad-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="581ad-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="581ad-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="581ad-107">Clean up deployment</span></span> 

<span data-ttu-id="581ad-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="581ad-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="581ad-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="581ad-109">Script explanation</span></span>

<span data-ttu-id="581ad-110">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="581ad-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="581ad-111">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="581ad-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="581ad-112">Comando</span><span class="sxs-lookup"><span data-stu-id="581ad-112">Command</span></span> | <span data-ttu-id="581ad-113">Note</span><span class="sxs-lookup"><span data-stu-id="581ad-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="581ad-114">az group create</span><span class="sxs-lookup"><span data-stu-id="581ad-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="581ad-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="581ad-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="581ad-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="581ad-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="581ad-117">Crea macchina virtuale hello e lo connette una scheda di rete toohello, rete virtuale, subnet e il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="581ad-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="581ad-118">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="581ad-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="581ad-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="581ad-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="581ad-120">Crea un tooallow di regola gruppo di sicurezza rete il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="581ad-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="581ad-121">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="581ad-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="581ad-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="581ad-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="581ad-123">Aggiunge e viene eseguito un tooa di estensione della macchina virtuale macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="581ad-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="581ad-124">In questo esempio, hello estensione della macchina virtuale Docker è tooconfigure usato un host Docker.</span><span class="sxs-lookup"><span data-stu-id="581ad-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="581ad-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="581ad-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="581ad-126">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="581ad-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="581ad-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="581ad-127">Next steps</span></span>

<span data-ttu-id="581ad-128">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="581ad-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="581ad-129">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="581ad-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
