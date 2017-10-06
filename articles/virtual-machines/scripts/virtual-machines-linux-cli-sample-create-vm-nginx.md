---
title: aaaAzure CLI Script di esempio - creare una VM Linux con NGINX | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con NGINX
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="d42cd-103">Creare una VM con NGINX</span><span class="sxs-lookup"><span data-stu-id="d42cd-103">Create a VM with NGINX</span></span>

<span data-ttu-id="d42cd-104">Questo script crea una macchina virtuale di Azure e Usa l'estensione Script personalizzata della macchina virtuale Azure di hello tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="d42cd-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="d42cd-105">Dopo l'esecuzione di script hello, è possibile accedere a un sito Web demo sull'indirizzo IP pubblico di hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d42cd-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d42cd-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d42cd-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="d42cd-107">Estensione di script personalizzati</span><span class="sxs-lookup"><span data-stu-id="d42cd-107">Custom Script Extension</span></span>

<span data-ttu-id="d42cd-108">estensione script personalizzata Hello copia questo script nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d42cd-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="d42cd-109">script di Hello viene quindi eseguito tooinstall e configurare un server web NGINX.</span><span class="sxs-lookup"><span data-stu-id="d42cd-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="d42cd-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d42cd-110">Clean up deployment</span></span> 

<span data-ttu-id="d42cd-111">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="d42cd-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d42cd-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d42cd-112">Script explanation</span></span>

<span data-ttu-id="d42cd-113">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d42cd-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d42cd-114">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="d42cd-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d42cd-115">Comando</span><span class="sxs-lookup"><span data-stu-id="d42cd-115">Command</span></span> | <span data-ttu-id="d42cd-116">Note</span><span class="sxs-lookup"><span data-stu-id="d42cd-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d42cd-117">az group create</span><span class="sxs-lookup"><span data-stu-id="d42cd-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d42cd-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="d42cd-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d42cd-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="d42cd-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d42cd-120">Crea macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="d42cd-120">Creates hello virtual machine.</span></span> <span data-ttu-id="d42cd-121">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="d42cd-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="d42cd-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="d42cd-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="d42cd-123">Crea un tooallow di regola gruppo di sicurezza rete il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="d42cd-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="d42cd-124">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="d42cd-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="d42cd-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="d42cd-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d42cd-126">Aggiunge e viene eseguito un tooa di estensione della macchina virtuale macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d42cd-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="d42cd-127">In questo esempio, un'estensione personalizzata hello è usato tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="d42cd-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="d42cd-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="d42cd-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d42cd-129">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="d42cd-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d42cd-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d42cd-130">Next steps</span></span>

<span data-ttu-id="d42cd-131">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d42cd-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d42cd-132">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d42cd-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
